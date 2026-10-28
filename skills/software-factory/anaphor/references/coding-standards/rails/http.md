# Rails HTTP boundary

## Choose the resource

Expose resources through dedicated controllers using `index`, `show`, `create`, `update`, or
`destroy`. Nested or singleton resources express a distinct owner or relationship. A controller may
have one action. Name the resource for its state; keep distinct operation contracts in separate
routes/actions instead of adding custom actions to a broad controller.

Each action calls one fixed, named use case, passes authenticated context and plain request data,
and maps its result to HTTP. Middleware and filters can reject unauthenticated requests, but the use
case still enforces user-scoped access. Controllers neither query nor mutate Active Record.

## Accept input

Keep request objects, route parameters, parsed JSON access, and rendering in controllers. Converting
a parsed body to a plain hash is transport work. Selecting accepted business fields, mapping nested
data, constructing cohesive input objects, and validating business facts belong to the use case.
Select explicit keys before persistence so extra request keys cannot mutate state.

Determine the caller contract before adding validation:

- A controlled frontend with agreed JSON types supplies numbers for IDs, arrays for collections,
  hashes for structured data, and strings for text. Trust that contract; validate presence, nonblank
  text, ownership, allowed transitions, exact ID membership, duplicate relationships, and revision
  preconditions. Unexpected shapes are caller defects.
- A public or external client boundary validates its documented schema at that boundary before
  passing stable values to business code. Apply actual supported protocol variants, rather than
  inventing coercions throughout the application.

Pass IDs directly to Active Record's attribute/query casting, including route parameters. Keep
numeric-string parsers, coercion-based type probes, and `NoMethodError`/`TypeError` rescues out of
business validation; they obscure broken caller contracts. See [arguments](../ruby/arguments.md) for
required use-case inputs.

## Render the outcome

Keep success/failure mapping visible in each action. Store the result in local `result`, leave one
blank line, then select the response. Repeat this small structure across actions rather than hiding
their response choices behind an inherited `render_result` dispatcher.

Render successful resource JSON through an action-specific Jbuilder view with
`locals: { result: result }`. Views read named result fields. Share small resource partials for
repeated fields; keep resource shapes out of large controller hashes and model-type serializers.
Promote a local to an instance variable only when the view needs it.

A feature result owns its endpoint `http_status` policy; the controller asks for it without decoding
failure codes or user-facing error text. Controllers retain template/body selection and may render a
small safe error envelope. The [result reference](results.md) owns the outcome contract.
