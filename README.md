# Jekyll Ideal Image Slider

Liquid tag plugin for Jekyll to create image sliders using  [Ideal Image Slider](https://github.com/gilbitron/Ideal-Image-Slider).

## Installation

1. Add `ideal_image_slider.rb` to your `_plugins` folder.

2. Add this to your `_config.yml` file: `slider_array: []`

3. Download and add [Ideal Image Slider](https://github.com/gilbitron/Ideal-Image-Slider) to your site. See below for [integration suggestions](#integration-suggestions).

## Syntax

```
{% slider height [captions] %}
{% endslider %}
```

## Usage

Surround a series of Markdown images with the following tag:

```
{% slider %}
  ![alt text 1](/img/image1.jpg)
  ![alt text 2](/img/image2.jpg)
  ![alt text 3](/img/image3.jpg)
{% endslider %}
```

The plugin will render the following html for you:

```
<div id="slider">
  <img src="/img/image1.jpg" alt="alt text 1">
  <img src="/img/image2.jpg" alt="alt text 2">
  <img src="/img/image3.jpg" alt="alt text 3">
</div>
```

You can add links to the images like this:

```
{% slider %}
  [![alt text 1](/img/image1.jpg)](/page/url)
  [![alt text 2](/img/image2.jpg)](/category/url)
  [![alt text 3](/img/image3.jpg)](http://example.com)
{% endslider %}
```

And the plugin will add a clickable link to each image in the slider:

```
<div id="slider">
  <a href="/page/url"><img src="/img/image1.jpg" alt="alt text 1"></a>
  <a href="/category/url"><img src="/img/image2.jpg" alt="alt text 2"></a>
  <a href="http://example.com"><img src="/img/image3.jpg" alt="alt text 3"></a>
</div>
```

You can define the height of a slider by placing a number or an aspect ratio after `slider`. If you don't specify  height, the slider will [default to `auto`](https://github.com/gilbitron/Ideal-Image-Slider#settings).

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
  ![this is the alt text](/img/image1.jpg)
  ![it will be used as a caption](/img/image2.jpg)
  ![for the image](/img/image3.jpg)
{% endslider %}
```

## Integration suggestions

Add the CSS to your page head template:

```
<!-- Slider CSS -->
<link rel="stylesheet" href="{{ site.baseurl }}/assets/css/slider.css">
<link rel="stylesheet" href="{{ site.baseurl }}/assets/css/theme.css">
```

Add the Javascript to your page template just before the `</body>` tag:

```
<!-- Slider -->
<script src="{{ site.baseurl }}/assets/js/slider.js"></script>
<script src="{{ site.baseurl }}/assets/js/iis-captions.js"></script>
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

Don't forget to change the locations to point towards wherever you have placed the Ideal Image Slider javascript and CSS files.

You can selectively include these files. The plugin sets `slider_active` to `true` for each page or post with a slider tag. Using the code below, CSS and Javascript will be loaded only for those pages with sliders, and on page indexes. (Sometimes an image slider will appear on a page index, especially if you're using excerpts.)

```
{% if page.slider_active or page.index %}
  <!-- Slider CSS -->
  <link rel="stylesheet" href="{{ site.baseurl }}/assets/css/slider.css">
  <link rel="stylesheet" href="{{ site.baseurl }}/assets/css/theme.css">
{% endif %}
```

```
{% if page.slider_active or page.index %}
  <!-- Slider -->
  <script src="{{ site.baseurl }}/assets/js/slider.js"></script>
  <script src="{{ site.baseurl }}/assets/js/iis-captions.js"></script>
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
