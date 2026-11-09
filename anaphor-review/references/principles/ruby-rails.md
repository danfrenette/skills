# Ruby and Rails

Read for changed Ruby responsibilities, collaborators, tests, or Rails workflows. These checks draw
on thoughtbot's Ruby Science and Sandi Metz. Treat them as design heuristics under the
[Principles procedure](README.md), not universal class or method size limits.

## Responsibilities and messages

**Trigger:** a class gains a decision, collaborator, or public method.

Trace who owns the state and who decides what to do with it. When callers repeatedly inspect another
object's state to make its business decision, consider moving that decision behind the owner's
interface. Show the callers coupled to the representation and the change that coupling would spread.

For changed orchestration, follow its private steps into collaborators. Identify the state owner,
decision owner, and representation the caller must understand. Assess concrete-class checks and
format branches against the actual collaborator contract; distinguish external-data validation from
inspecting known collaborators. A readable entry point or a single workflow name does not establish
cohesive ownership. Report the coupling found, or the inspected boundary that justifies keeping the
decision in place. Existing result protocols can legitimately require success/failure checks; assess
the operation they guard rather than treating every query as a violation.

Keep Rails presentation decisions in their presentation layer; moving rendering into a model merely
to eliminate a query increases coupling. Sources: thoughtbot's [Tell, Don't Ask][tell] and [Single
Responsibility Principle][srp].

## Abstractions supported by real variation

**Trigger:** shared code gains flags, caller-specific branches, or a new inheritance/mixin layer.

Compare the actual callers. Identify whether they share one responsibility or only similar syntax.
If each caller now selects a different subset of the abstraction, consider separating their paths
before extending it. Name which dependency or conditional disappears. This is not a mandate to
duplicate stable shared behavior or prebuild a framework for hypothetical variation. Source: Sandi
Metz's [The Wrong Abstraction][abstraction].

## Composition with an explicit contract

**Trigger:** a concern, mixin, or superclass adds behavior that depends on host state or method
order.

List the host methods/state the behavior assumes. Check whether those hidden requirements make a
second caller or isolated test difficult. Propose an explicit collaborator only when it reduces
those obligations. A small cohesive concern using established Rails conventions does not require
replacement merely because it is a mixin. Source: thoughtbot's [Replace Mixin with
Composition][mixin].

## Rails reads and query composition

**Trigger:** a facade, read service being replaced, query object, or relation extension changes.

Resolve the applicable coding standards first. When the Anaphor Rails fallback applies, check the
[required query convention](../../../anaphor/references/coding-standards/rails/queries.md) and the
[facade boundary](../../../anaphor/references/coding-standards/rails/facades.md), and report
breaches through Standards. A named module extending an `ActiveRecord::Relation` has an explicit
framework interface; preserve that convention when considering mixin alternatives.

Trace the authorized input through filters, joins, and subqueries, then follow execution into the
facade loading entry. Check that omitted filters preserve the selection and that presentation
receives completed data. Distinguish a relation-returning query from a documented
aggregate/data-returning query before applying the extension requirement. Assess the ownership and
scope contract rather than treating the module's presence alone as evidence of good composition.
Sources: thoughtbot's [A Case for Query Objects in Rails][queries] and Active Record's [`extending`
API][extending].

A facade coordinates read-only data; a service owns a mutation workflow, including its necessary
reads. Check facade readers for hidden I/O or writes and keep index query composition below the
facade. The service/facade division is an adopted convention, not a universal restriction of the
Facade design pattern. thoughtbot's [open-source page example][facades] illustrates a read facade.

## Rails workflow visibility

**Trigger:** callbacks start or expand a business workflow or external side effect.

Trace what each save/update caller now triggers, including callers that only intend persistence.
Check whether an explicit operation would make sequencing and failure handling clearer. Distinguish
record lifecycle invariants from actions the caller should choose. Trace transaction/retry defects
through Execution or the relevant risk pass rather than presenting them only as style concerns.
Source: thoughtbot's [Replace Callback with Method][callback].

## Loading more guidance

Use a project-named Ruby/Rails design or testing skill when it covers the changed concern. Confirm
its provenance instead of assuming a skill named for an author exists. Use the linked source section
when local questions need expansion; consult documentation for the project's Rails version before
recommending framework-specific behavior. Keep behavior-test quality aligned with the adopted `tdd`
discipline rather than introducing a competing testing workflow here.

Primary sources checked 2026-10-04:

[tell]: https://thoughtbot.com/ruby-science/tell-dont-ask.html
[srp]: https://thoughtbot.com/ruby-science/single-responsibility-principle.html
[abstraction]: https://sandimetz.com/blog/2016/1/20/the-wrong-abstraction
[mixin]: https://thoughtbot.com/ruby-science/replace-mixin-with-composition.html
[callback]: https://thoughtbot.com/ruby-science/replace-callback-with-method.html

Query sources checked 2026-10-28:

[queries]: https://thoughtbot.com/blog/a-case-for-query-objects-in-rails
[extending]: https://api.rubyonrails.org/classes/ActiveRecord/QueryMethods.html#method-i-extending

Facade source checked 2026-10-30:

[facades]: https://thoughtbot.com/blog/a-peek-behind-the-curtain-of-our-new-open-source-page
