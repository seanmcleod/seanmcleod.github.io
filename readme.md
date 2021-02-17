# How To

Generate a new post.

```sh
hugo new post/post-name.md
```

If post has images then create an image directory for it.

```sh
mkdir static\image\post-name
```

Use Visual Studio to edit the new post's markdown file in:

```sh
content\posts\post-name.md
```

Run the Hugo server while editing.

```sh
hugo server
```

When complete quit hugo server and run hugo to generate static files.

```sh
hugo
```

Then add modified and new files to git, commit and push.

```sh
git add .
git commit -m "New post - Post Name"
git push
```

The git push to github will kick off a process on github to publish the changes.

Profit.
