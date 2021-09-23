# Semver Governance Model

The "RFC" (request for comments) process is intended to provide a consistent and controlled path for changes to the SemVer specification, so that all stakeholders can be confident about the direction the spec is evolving in.

## When you need to follow this process

You need to follow this process if you intend to make "substantial" changes to the specification or the RFC process itself. What constitutes a "substantial" change is evolving based on community norms and varies depending on what part of the specification you are proposing to change, but may include the following:

* Changes to the meaning of the specification.

Some changes do not require an RFC:

* Typo fixes
* Small wording clarifications that do not impact the semantics of the specification.

## What the process is

When a pull request ("PR" from here forward) is opened against the specification or
this repository, it may be tagged with an "RFC" tag ("RFC" from here forward).
RFCs require the consensus of all team members (see below) to merge.

## The SemVer Team

We welcome feedback from anyone on the direction of SemVer. However, a group of people, "the SemVer team," are responsible for making decisions about RFC PRs. The SemVer team is made up of representatives from package managers that use SemVer. 

Team members are added and removed based on the consensus of the existing team members. The @semver/maintainers team on GitHub contains the official list of the members of "the SemVer team."

The maintainers are:

* [anangaur](https://github.com/anangaur) ([NuGet](https://www.nuget.org/))
* [dherman](https://github.com/dherman) ([Notion](https://www.notionjs.com/))
* [indirect](https://github.com/indirect) ([Bundler](https://bundler.io/))
* [isaacs](https://github.com/isaacs) ([npm](https://www.npmjs.com/))
* [segiddins](https://github.com/segiddins) ([CocoaPods](https://cocoapods.org/))
* [steveklabnik](https://github.com/steveklabnik) ([Cargo](https://crates.io/))
* [Seldaek](https://github.com/Seldaek) ([Composer](https://getcomposer.org/))

## Participation commitment

Participation in the SemVer governance process requires a commitment to maintain, to the greatest degree possible, consistency of the functional and semantic interoperability between SemVer implementations. Towards that end:

* RFCs will be considered formally adopted only when they are approved by the SemVer Maintainers group, _and_ implemented in a simple majority of represented implementations.
* No RFC will be approved if it is deemed to cause significant breakage to any of the SemVer-using  communities represented by the SemVer Maintainers group.  It is the responsibility of the SemVer Maintainers group to advocate for their communities in good faith.
* With the understanding that implementation may present challenges and require time to complete, refusal on principle to implement approved RFCs will result in removal from the group.
* Implementations may add functionality in advance of an approved RFC (in fact, they have to!) but all such functionality must be flagged as "experimental", so that users understand it may change in the future.  (Maintainers are encouraged to perform these experimental changes on forks rather than the implementation in use by their package management communities, to reduce the chance of users coming to rely on experimental functionality.)

## The lifecycle of an RFC

Once a PR is tagged as an RFC:

* The author of the PR should build consensus and integrate feedback. RFCs that have broad support are much more likely to make progress than those that don't receive any comments. Feel free to reach out to the team members to get help identifying stakeholders and obstacles.
* The team will discuss the RFC, as much as possible in the comment thread of the pull request itself. Offline discussion will be summarized on the pull request comment thread.
* RFCs rarely go through this process unchanged. You can make edits, big and small, to the RFC to clarify or change the design, but make changes as new commits to the pull request, and leave a comment on the pull request explaining your changes. Specifically, do not squash or rebase commits after they are visible on the pull request.
* At some point, a member of the team will propose a "motion for final comment period" (FCP), along with a disposition for the RFC (merge, close, or postpone).
    * This step is taken when enough of the tradeoffs have been discussed that the subteam is in a position to make a decision. That does not require consensus amongst all participants in the RFC thread (which is usually impossible). However, the argument supporting the disposition on the RFC needs to have already been clearly articulated, and there should not be a strong consensus against that position outside of the subteam. Subteam members use their best judgment in taking this step, and the FCP itself ensures there is ample time and notification for stakeholders to push back if it is made prematurely.
    * For RFCs with lengthy discussion, the motion to FCP is usually preceded by a summary comment
    trying to lay out the current state of the discussion and major tradeoffs/points of disagreement.
    * Before actually entering FCP, all members of the subteam must sign off; this is often the point at which many subteam members first review the RFC in full depth.
* The FCP lasts ten calendar days, so that it is open for at least 5 business days. This way all stakeholders have a chance to lodge any final objections before a decision is reached.
* In most cases, the FCP period is quiet, and the RFC is either merged or closed. However, sometimes substantial new arguments or ideas are raised, the FCP is canceled, and the RFC goes back into development mode.

## RFC postponement

Some RFC pull requests are tagged with the "postponed" label when they are closed (as part of the rejection process). An RFC closed with "postponed" is marked as such because we want neither to think about evaluating the proposal nor about implementing the described feature until some time in the future, and we believe that we can afford to wait until then to do so. Postponed pull requests may be re-opened when the time is right. We don't have any formal process for that, you should ask members of the team.

Usually an RFC pull request marked as "postponed" has already passed an informal first round of evaluation, namely the round of "do we think we would ever possibly consider making this change, as outlined in the RFC pull request, or some semi-obvious variation of it." (When the answer to the latter question is "no", then the appropriate response is to close the RFC, not postpone it.)
