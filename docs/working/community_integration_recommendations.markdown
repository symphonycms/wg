#Symphony Community+Docs Integration Proposal#

Many members of the Symphony community have expressed frustration about the lack of tools for contributing to documentation. As a result, the forums have become overcrowded with material that should be extracted into the official docs. In addition, beginner questions are mixed together with more complex discussions, and this makes navigating the forums difficult.

The Docs WG [brainstormed](http://github.com/jonasd/docs/blob/master/working/community_integration_brainstorm.markdown) and considered several approaches to improve the community's ability to write unique content and contribute to the official documentation. Our focus was to provide the best results with the least amount of structural or functional changes to the existing Symphony website.

##Recommendation 1: Provide a "Question" forum discussion category.##

This functionality would work as follows:

*	User creates a new discussion.
*	In the Category dropdown, user selects "Question" (or "How-To" / "Help Request.") *Note: fields for "Question" discussions may differ from the other categories.*
*	Once submitted, "Question" discussions would allow user voting on replies, similar to Stack Overflow or Engadget's comments. Best-rated responses would be promoted to the top.

Benefits resulting from the change:

*	The community can rank responses, helping future searchers locate the best answers easily.
*	The Docs WG could easily mine the best-rated items for the official FAQ (or potentially build the FAQ programmatically.)
*	The additional Category would provide an easy distinction between support conversations and conceptual conversations in the forums.
*	With the possible exception of the voting functionality, implementing this would not be too difficult.

##Recommendation 2: Allow community Suggestions and Contributions on the official documentation.##

This functionality would work as follows:

*	Each documentation asset (Tutorial, Article, Concept, etc) would have options for users to "Suggest Improvements" or "Contribute an Example." 
*	Each asset would also have links to browse the existing open suggestions and contributions.
*	These items would function similar to the issue tracker — suggestions and examples will be reviewed, integrated (or not), and closed by the Docs group.

Benefits resulting from the change:

*	Community review and contribution will improve the documentation, reducing the maintenance burden of the docs group.
*	The Symphony Team retains editorial control of official documentation.
*	Better docs = less forum discussions = less clutter in the forums.

##Recommendation 3: Provide better ways for the community to submit original content.##

This recommendation is not fully baked, but the notion is that we should have an easy submission option for people who write original content suitable for the official docs. A good example is [Stephen's lengthy post about Git workflow](http://symphony-cms.com/discuss/thread/47779/#position-8).

In addition to providing a submission capability, we would need to create some basic guidelines (style, formatting, etc) and/or a standardized template.

This solution could be as simple as "download this Markdown template and submit your finished document to docs@symphony-cms.com." But we also need to provide solutions for embedded images, video, etc.
