# review-saperlipopette

Editor for rOpenSci software review of {saperlipopette} 

Review: https://github.com/ropensci/software-review/issues/754

Upon submission

* [ ] check output from ropensci-review-bot
* [X] check issue template has been properly filled out. Editors can edit directly for minor fixes or ask authors for to fill any fields that may be missing
* [X] check statistical properties including noteworthy (especially eg. loc and n_fns_...) 
* [X] check network visualisation of calls between objects:
  * [X] check if package has too few functions or lines of code, in which case it may be insufficiently developed for peer review.
  * [X] check if package is extremely large, in which case it may be too burdensome for reviewers. For example, these initial checks revealed a package with over 8,500 lines of R code (corresponding to 97.6% of all packages), and 251 exported R functions.


Initial editorial comments

* [X] use the editor template to guide initial checks (within 5 working days)
* [X] check against policies for fit and overlap
* [X] ensure that the package gets tested on multiple platforms 
* [X] wherever possible when asking for changes, direct authors to automatic tools (eg. Air)
* [X] if initial checks show major gaps, request changes before assigning reviewers, consider applying holding label by calling @ropensci-review-bot put on hold

Look for and assign two reviewers

* [ ] `@ropensci-review-bot seeking reviewers`
* [ ] use the email template if needed for inviting reviewers
* [ ] check [finding reviewers](https://devguide.ropensci.org/softwarereview_editor.html#look-for-and-assign-two-reviewers) for finding reviewers
* [ ] check [criteria for choosing a reviewer](https://devguide.ropensci.org/softwarereview_editor.html#criteria-for-choosing-a-reviewer)

Assign reviewers

* [ ] `@ropensci-review-bot assign @username as reviewer`
* [ ] if you want to change the due date for a review use `@ropensci-review-bot set due date for @username to YYYY-MM-DD`

During review

* [ ] Upon each review being submitted,
  * [ ] Write a comment thanking the reviewer in your own words.
  * [ ] Record the review by typing a new comment `@ropensci-review-bot submit review <review-url> time <time in hours>`
* [ ] upon changes being made, change the review status tag to 5/awaiting-reviewer-response, and request that reviewers indicate approval with the reviewer approval template

After review

* [ ] `@ropensci-review-bot approve <package-name>`

Package promotion

* [ ] direct the author to the chapters of the guide about package releases, marketing and GitHub grooming

## Resources

https://devguide.ropensci.org/softwarereview_editor.html

