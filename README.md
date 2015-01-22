---
languages: html, css
tags: git, todo
resources: 2
---

# Git Merge Conflicts

![What Did I Tell You](http://www.geekynews.com/pub/wp-content/uploads/2013/09/lloyd-back-to-the-future-439x247.jpg)

## Introduction

Marty McFly and Doc Brown just finished their student profiles. Now they need to merge their profiles into the `master` branch, so that they'll have a completed profile page.

__This is what we will be working towards:__

![The Goal](https://s3-us-west-2.amazonaws.com/web-dev-readme-photos/git-merge-conflicts/goal)

## Merging Git Branches

On our `master` branch, we have a placeholder profile in place. Marty's finished profile is stored in the `marty-mcfly` branch. Doc's is in the `doc-brown` branch. We are going to merge both branches onto a new branch and resolve the merge conflicts there before putting it all back on the master branch.

### Step 1: Make sure you have both branches

Make sure you are in the `master` branch.
- run `git branch` in the terminal, while you're in the "git-merge-conflicts folder, to see all of the branches."

The output should look like this:

```bash
$ git branch
* master
  doc-brown
  marty-mcfly
```

If you do not see the `doc-brown` or `marty-mcfly` branch, you will need to grab it from Github (also known as `origin`).
- run `git checkout -t origin/doc-brown`
- run `git checkout -t origin/marty-mcfly`
(This creates a new branch on your computer that matches the`doc-brown` and `marty-mcfly` branches on GitHub)

Now your output should include both branches. (run `git branch` again to check. If you don't have both branches, grab an instructor or ask a teammate for help.)


### Step 2: Navigate into the `master` branch

Check out the `master` branch:
- run `git checkout master`

You should now be in the `master` branch.

 _(Remember: you can check by running `git branch`)_

### Step 3: Merge!

From the `master` branch, merge the branches via `git merge <branch name>`. Let's merge the `doc-brown` branch by running `git merge doc-brown` in our Terminal.

When you merge `doc-brown` into your `master` branch, your Terminal should print a readout that looks like this:

```unix
Updating 4040eed..cd5fd46
Fast-forward
 img/students/doc_brown_index_profile.jpg    | Bin 0 -> 32589 bytes
 img/students/student_name_background.jpg    | Bin 72485 -> 0 bytes
 img/students/student_name_index_profile.jpg | Bin 17565 -> 0 bytes
 img/students/student_name_profile.jpg       | Bin 12632 -> 0 bytes
 index.html                                  |  20 +++++++++++++++++++-
 5 files changed, 19 insertions(+), 1 deletion(-)
 create mode 100644 img/students/doc_brown_index_profile.jpg
 delete mode 100644 img/students/student_name_background.jpg
 delete mode 100644 img/students/student_name_index_profile.jpg
 delete mode 100644 img/students/student_name_profile.jpg
```

Awesome! You've merged all of Doc Brown's profile information into the `master` branch! Let's take a look at the index page by running `open index.html` in our Terminal. It's important to keep looking at index.html to make sure that it looks exactly how we want it to look, and also to make sure that nothing funky or weird is happening. 

__The `index.html` page should look like this:__

![Doc Brown Merge](https://s3-us-west-2.amazonaws.com/web-dev-readme-photos/git-merge-conflicts/add-doc-brown)

Now let's try merging in Marty McFly's profile information into `master`. Ensure that you are currently on your `master` branch. In your Terminal, run `git merge marty-mcfly`. Perhaps it will go swimmingly.... or __will it__?

Ahhhhh, wait!!! There's a merge conflict!

```
Auto-merging index.html
CONFLICT (content): Merge conflict in index.html
Automatic merge failed; fix conflicts and then commit the result.
```

__This is what `index.html` should look like with the merge conflict:__

![Merge Conflict!](https://s3-us-west-2.amazonaws.com/web-dev-readme-photos/git-merge-conflicts/merge-conflict)

### Step 4: Fix the conflicts

Open up the `index.html` file. Scroll down to around line 93. You should see something that looks like this:

```html
<<<<<<< HEAD
              <!-- Begin Profile -->
              <li class="home-blog-post">
                <div class="blog-thumb">
                  <img width="304" height="304" class="prof-image" src="img/students/doc_brown_index_profile.jpg" class="attachment-blog-thumb wp-post-image" alt="doc brown">
                </div>

               <div class="blog-title">
                  <div class="big-comment">
                    <h3>Doc Brown</h3>
                  </div>
                  <p class="home-blog-post-meta">"Great Scott!"</p>
                </div>
                <div class="clear"></div>

                <div class="excerpt">
                  <p>Doctor Emmett Lathrop "Doc" Brown was the inventor of the DeLorean time machine. Doc's role models were scientists, as evidenced by the names of his dogs and the portraits of Isaac Newton and Albert Einstein found inside his laboratory.</p>
                </div>
                <div class="clear"></div>
              </li>
              <!-- End Profile -->
              
=======
>>>>>>> marty-mcfly

... (MORE CODE) ...

```
#### What does it mean!?

Git does its best to merge the code, but sometime sit just doesn't work. We need to complete the merge ourselves by manually adjusting the code. Git gives us a few hints to help us out:

 `<<<<<<< HEAD` - the beginning of the original branch (`master`)
 `=======` - the end of the original branch/the begining of the branch being merged in (`marty-mcfly`)
 `>>>>>>> marty-mcfly` - the end of the new branch ( `marty-mcfly`)

Take your time and shift the code around, separating the `MARTY MCFLY` and `DOC BROWN` code blocks. Use the markers from  git as a guide.

_Hint: You can also use the HTML tags as guides. If one section ends with an opening `<a>` tag, look for the closing `</a>` tag in the next section._

When you're done the code should look something like this:

 ```html
<!-- Begin MARTY MCFLY -->
<li class="home-blog-post">
  <div class="blog-thumb">
    <a href="students/marty_mcfly.html">
      <img width="304" height="304" class="prof-image" src="img/students/marty_mcfly_index_profile.jpg" class="attachment-blog-thumb wp-post-image" alt="doc brown">
    </a>
  </div>

... (MORE CODE) ...

</li>
<!-- End MARTY MCFLY -->

<!-- Begin DOC BROWN -->
<li class="home-blog-post">
  <div class="blog-thumb">
    <a href="students/doc_brown.html">
      <img width="304" height="304" class="prof-image" src="img/students/doc_brown_index_profile.jpg" class="attachment-blog-thumb wp-post-image" alt="doc brown">
    </a>
  </div>

... (MORE CODE) ...

</li>
<!-- End DOC BROWN -->
 ```

If everything is looking good, we're ready to commit the changes before moving on.
- run `git add index.html` to add all of the changes made in `index.html` to the stage.
- run `git commit -am "merge marty and doc index pages"`.


### Step 5: You're Almost There!

Almost done! The next and last step is to confirm that the `master` branch has everything we need.

Confirm that `index.html` in the `master` branch has the following for both Doc Brown and Marty McFly:
- profile images
- profile names
- descriptions

Once we have that, we can then delete the `doc-brown` and `marty-mcfly` branches:
- run `git branch -D doc-brown` to delete the `doc-brown` branch.
- run `git branch -D marty-mcfly` to delete the `marty-mcfly` branch.

That's it! Open up `index.html` in your browser to see your beautiful work!

![YAY](http://media0.giphy.com/media/bhrxcjDGsnGq4/200.gif)
## Resources

- [Git Branching - Basic Branching and Merging](http://git-scm.com/book/en/Git-Branching-Basic-Branching-and-Merging)
- [Stack Overflow - Best (and safest) way to merge a git branch into master](http://stackoverflow.com/questions/5601931/best-and-safest-way-to-merge-a-git-branch-into-master)
