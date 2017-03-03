# Jekyll Ideal Image Slider

Liquid tag plugin to add image sliders to Jekyll with [Ideal Image Slider](https://github.com/Codeinwp/Ideal-Image-Slider-JS). This plugin is not compatible with Github Pages. Use [Jekyll Ideal Image Slider Include](https://github.com/jekylltools/jekyll-ideal-image-slider-include) for Github Pages compatibility.

## Installation

1. Add [`_plugins/ideal_image_slider.rb`](_plugins/ideal_image_slider.rb) to your `_plugins` folder.

2. Add this line to your `_config.yml` file: `slider_array: []`

3. Add [Ideal Image Slider](https://github.com/Codeinwp/Ideal-Image-Slider-JS) to your site, either manually or using Bower.

4. See below for [integration suggestions](#integration-suggestions).

## Syntax

```
{% slider height [captions] %}
{% endslider %}
```

## Usage

Surround a series of Markdown images with the following tag:

```
{% slider %}
  ![alt text 1](image1.jpg)
  ![alt text 2](image2.jpg)
  ![alt text 3](image3.jpg)
{% endslider %}
```

The plugin will render the following html for you:

```
<div id="slider">
  <img src="image1.jpg" alt="alt text 1">
  <img src="image2.jpg" alt="alt text 2">
  <img src="image3.jpg" alt="alt text 3">
</div>
```

You can add links to the images like this:

```
{% slider %}
  [![alt text 1](image1.jpg)](/page/url)
  [![alt text 2](image2.jpg)](/category/url)
  [![alt text 3](image3.jpg)](http://example.com)
{% endslider %}
```

And the plugin will add a clickable link to each image in the slider:

```
<div id="slider">
  <a href="/page/url"><img src="image1.jpg" alt="alt text 1"></a>
  <a href="/category/url"><img src="image2.jpg" alt="alt text 2"></a>
  <a href="http://example.com"><img src="image3.jpg" alt="alt text 3"></a>
</div>
```

You can define the height of a slider by placing a number or an aspect ratio after `slider`. If you don't specify  height, the slider will [default to `auto`](https://github.com/Codeinwp/Ideal-Image-Slider-JS#settings).

```
{% slider 700 %}
{% slider 4:3 %}
{% slider auto %}
```

If you add `captions` after the height variable, it will enable captions for the slider. The alt text of an image will be used as a caption for that image:

```
{% slider captions %}
{% slider 480 captions %}
```
```
{% slider captions %}
  ![this is the alt text](image1.jpg)
  ![it will be used as a caption](image2.jpg)
  ![for the image](image3.jpg)
{% endslider %}
```

## Integration suggestions

Add the CSS to your page head template:

```
<!-- Slider CSS -->
<link rel="stylesheet" href="{{ "/assets/css/slider.css" | relative_url }}">
<link rel="stylesheet" href="{{ "/assets/css/theme.css" | relative_url }}">
```

Add the Javascript to your page template just before the `</body>` tag:

```
<!-- Slider -->
<script src="{{ "/assets/js/slider.js" | relative_url }}"></script>
<script src="{{ "/assets/js/iis-captions.js" | relative_url }}"></script>
<!-- Sliders on pages -->
{% for script in page.slider_scripts %}
  {{ script }}
{% endfor %}
<!-- Sliders on indexes -->
{% for post in paginator.posts %}
  {% for script in post.slider_scripts %}
    {{ script }}
  {% endfor %}
{% endfor %}
```

Be sure to change the paths to the correct location of the Javascript and CSS files in your site.

You can selectively include these files. The plugin sets `slider_active` to `true` for each page or post with a slider. Using the code below, CSS and Javascript will be loaded only for those pages with sliders.

```
{% if page.slider_active %}
  <!-- Slider CSS -->
  <link rel="stylesheet" href="{{ "/assets/css/slider.css" | relative_url }}">
  <link rel="stylesheet" href="{{ "/assets/css/theme.css" | relative_url }}">
{% endif %}
```

```
{% if page.slider_active %}
  <!-- Slider -->
  <script src="{{ "/assets/js/slider.js" | relative_url }}"></script>
  <script src="{{ "/assets/js/iis-captions.js" | relative_url }}"></script>
  <!-- Sliders on pages -->
  {% for script in page.slider_scripts %}
    {{ script }}
  {% endfor %}
  <!-- Sliders on indexes -->
  {% for post in paginator.posts %}
    {% for script in post.slider_scripts %}
      {{ script }}
    {% endfor %}
  {% endfor %}
{% endif %}
```

## Support

[Open an issue](https://github.com/jekylltools/jekyll-ideal-image-slider/issues) if you have any problems, questions or suggestions for improvement.
