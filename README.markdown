## Steps to create new blog post

``` ruby
rake new_post['new post title']
```

This will create new file in folder source/_posts. Draft that file to create post content. 

To generate HTML content, use command
``` ruby
rake generate
```

To preview HTML content in local, use following command and open http://localhost:4000 in the browser
``` ruby
rake preview
```

To deploy new post, use command
``` ruby
rake deploy
```

To submit blog source code to github server, use command
``` bash
git add *
git commit -m "commit message"
```

