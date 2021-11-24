# NLIWoD workshop homepage

This repo utilizes the [minimal mistakes](https://jekyllthemes.io/theme/minimal-mistakes) jekyll theme. Their [documentation](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/) is very comprehensive.


## Past workshops and navbar
This year's workshop website is defined at the top level of this repo. The past websites are linked internally via the navbar and located in the ```past-workshops``` folder.
To add pages to the navbar go to ```_data/navigation.yml``` and simply add page title and url to the list.

## Customizing/adding pages 
The top-level markdown files are the pages that you see on the website (```index.md``` is the home page). 
To add a new page, just create a new markdown file and make sure to list it in ```_data/navigation.yml```.

The main configuration file ```_config.yml``` gives you more options for customization. You can, e.g., change the main title and tagline there. 
If you'd like to change the image in the header, load a new image into the ```assets``` folder and then adjust the path here:
```
header:
    overlay_image: /assets/images/nasa-1lfI7wkGWZ4-unsplash.jpeg
    overlay_filter: rgba(0, 0, 0, 0.2)
    caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
```

Within a page, you may overwrite the defaults in ```_config.yml```. For example, in ```index.md```, the header is overwritten to include a link:
```
---
header:
  actions:
    - label: "Co-located with the 21st International Semantic Web Conference (ISWC)"
      url: "http://iswc2022.semanticweb.org/"
---
```

