# Git Merge Conflicts

![What Did I Tell You](http://www.geekynews.com/pub/wp-content/uploads/2013/09/lloyd-back-to-the-future-439x247.jpg)

## Introduction

Marty McFly and Doc Brown just finished their student profiles. Now they need to merge their profiles into the `master` branch, so that they'll have a completed profile page.

__This is what we will be working towards:__

![The Goal](https://s3-us-west-2.amazonaws.com/web-dev-readme-photos/git-merge-conflicts/goal)

## Merging Git Branches

On the `master` branch, there is a placeholder profile in place. The index page on that branch looks like this:

![avatar-placeholder-master-branch](https://s3-us-west-2.amazonaws.com/web-dev-readme-photos/git-merge-conflicts/master-branch)

Doc's finished profile is in the `doc-brown` branch. The index page on his branch looks like this:

![doc-browns-branch](https://s3-us-west-2.amazonaws.com/web-dev-readme-photos/git-merge-conflicts/doc-brown-branch)

Meanwhile, Marty's finished profile is stored in the `marty-mcfly` branch. His index page on his branch looks like this:

![marty-mcflys-branch](https://s3-us-west-2.amazonaws.com/web-dev-readme-photos/git-merge-conflicts/marty-mcfly-branch)

You are going to merge both branches onto the master branch and resolve the merge conflicts when needed.

To accomplish this, you're going to be following six steps, overviewed below:

1. Make sure you have all three branches
2. Switch to the master branch
3. Merge Doc's branch into the master branch, then merge Marty's branch in
4. Fix the merge conflict
5. Delete Doc and Marty's branches on your computer
6. Push up your work and submit a pull request

### Step 1: Make sure you have both branches

Remember to fork then clone down this repo. Then change directories into it:

* `cd git-merge-conflicts-< your semester name >`

The first step is to see how many branches you have locally. Run `git branch` from your terminal to see all of the branches. The output should look like this:

```bash
$ git branch
* master
```

To fetch the  `doc-brown` or `marty-mcfly` branches, run the following commands in order:

* `git checkout -t origin/doc-brown`
* `git checkout -t origin/marty-mcfly`

This creates a new branch on your computer that matches the`doc-brown` and `marty-mcfly` branches on GitHub. Now your output should include both branches. But don't take this readme's word for it: run `git branch` again to double check. The output should look like this:

```bash
$ git branch
  doc-brown
* marty-mcfly
  master
```

If you don't have all three branches, ask a teammate for help.

As you can tell, the marty-mcfly branch is starred and highlighted. This is Git's way of telling you which branch you're on. Therefore, you're on the marty-mcfly branch.

### Step 2: Navigate into the `master` branch

Remember, checkout allows you to switch between branches that are on your local machine. It's time to check out the `master` branch:

- `git checkout master`

You should now be in the `master` branch. Remember, you can confirm you're on the master banch if it's starred and highlighted when you run `git branch`:

```bash
$ git branch
  doc-brown
  marty-mcfly
* master
```

From the master branch, run `open index.html` from your terminal, you should see a web page with just a placeholder avatar. Marty and Doc should not be there.

### Step 3: Merge!

You're going to add both the doc-brown branch and the marty-mcfly branch to the master branch using merge. Merge the `doc-brown` branch first by running `git merge doc-brown` in the terminal.

When you merge `doc-brown` into your `master` branch, your terminal should print a readout that looks something like this:

```bash
Updating 7d220f6..bb73c64
Fast-forward
 img/students/doc_brown_index_profile.jpg    | Bin 0 -> 32589 bytes
 img/students/student_name_background.jpg    | Bin 72485 -> 0 bytes
 img/students/student_name_index_profile.jpg | Bin 17565 -> 0 bytes
 img/students/student_name_profile.jpg       | Bin 12632 -> 0 bytes
 index.html                                  |  23 ++++++++++++++++++++++-
 5 files changed, 22 insertions(+), 1 deletion(-)
 create mode 100644 img/students/doc_brown_index_profile.jpg
 delete mode 100644 img/students/student_name_background.jpg
 delete mode 100644 img/students/student_name_index_profile.jpg
 delete mode 100644 img/students/student_name_profile.jpg
 ```

This readout confirms that you've merged all of Doc Brown's profile information into the `master` branch. Take a look at the index page by again running `open index.html` in the terminal. It's important to keep looking at `index.html` to make sure that it looks exactly how you want it to look.

__The `index.html` page should look like this:__

![Doc Brown Merge](https://s3-us-west-2.amazonaws.com/web-dev-readme-photos/git-merge-conflicts/add-doc-brown)

Now try merging in Marty McFly's profile information into the master branch. You probably already are, but ensure that you are currently on your `master` branch (type `git branch`). Then run `git merge marty-mcfly`. Perhaps it will go swimmingly.... or __will it__?

Ahhhhh, wait!!! There's a merge conflict!

```
Auto-merging index.html
CONFLICT (content): Merge conflict in index.html
Automatic merge failed; fix conflicts and then commit the result.
```

__This is what `index.html` should look like with the merge conflict:__

![Merge Conflict!](https://s3-us-west-2.amazonaws.com/web-dev-readme-photos/git-merge-conflicts/merge-conflict)

### Step 4: Fix the conflicts

Open up the `index.html` file. Scroll down to around line 114 and 137. You should see something that looks like this:

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

Git does its best to merge the code, but sometimes it just doesn't work. You need to complete the merge yourself by manually adjusting the code. Git gives you a few hints to help us out:

* `<<<<<<< HEAD` - the beginning of the original branch (`master`)
* `=======` - the end of the original branch/the beginning of the branch being merged in (`marty-mcfly`)
* `>>>>>>> marty-mcfly` - the end of the new branch ( `marty-mcfly`)

Take your time and shift the code around, separating the `MARTY MCFLY` and `DOC BROWN` code blocks. Use the markers from git as a guide.

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

Remember, you can open the index page by running `open index.html`. The page should look like the picture at the very top of this readme.

If everything is looking good, we're ready to commit the changes before moving on.
- run `git add .` to stage all changes made in `index.html`
- run `git commit -am "merge marty and doc index pages"` to commit, or finalize, these changes

### Step 5: You're Almost There!

Almost done! The next and last step is to confirm that the `master` branch has everything we need.

Confirm that `index.html` in the `master` branch has the following for both Doc Brown and Marty McFly:

- profile images
- profile names
- descriptions

Once you have that, make sure you're still on the master branch. Now delete the `doc-brown` and `marty-mcfly` branches:

- run `git branch -D doc-brown` to delete the `doc-brown` branch
- run `git branch -D marty-mcfly` to delete, you guessed it, the `marty-mcfly` branch

That's it! Open up `index.html` in your browser to see your beautiful work!

![YAY](http://i.giphy.com/J1WfRHBFj8lFK.gif)

### Step 6: Finish Up

Remember, while your computer has these updates, GitHub has no idea that you made them. Remember to push up your changes to your remote repo and to submit a pull request!

From the master branch, run:

* `git push origin master`
* Go to your forked repo (the url will look something like `http://github.com/< your GitHub username>/git-merge-conflicts-<your semester name>`, but you can also get there by going to your GitHub account and clicking on `repos`)
* Click on the green pull request button, add a title, a description if you'd like, and click "submit pull request"

Congrats on fixing your first merge conflict!

## Resources

- [Git Branching - Basic Branching and Merging](http://git-scm.com/book/en/Git-Branching-Basic-Branching-and-Merging)
- [Stack Overflow - Best (and safest) way to merge a git branch into master](http://stackoverflow.com/questions/5601931/best-and-safest-way-to-merge-a-git-branch-into-master)


<<<<<<< HEAD
<p data-visibility='hidden'>View <a href='https://learn.co/lessons/git-merge-conflicts' title='Git Merge Conflicts'>Git Merge Conflicts</a> on Learn.co and start learning to code for free.</p>
=======
<a href='https://learn.co/lessons/git-merge-conflicts' data-visibility='hidden'>View this lesson on Learn.co</a>
>>>>>>> 2dcc095752770d57481f4b5d4fac9b8d3949e161
