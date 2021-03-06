## SeleniumBase Website Tours

SeleniumBase Tours utilize your choice of 4 different JavaScript libraries for creating & running tours, demos, and walkthroughs on any website: **[Shepherd](https://shipshapecode.github.io/shepherd/docs/welcome/)**, **[Bootstrap Tour](http://bootstraptour.com/)**, **[IntroJS](https://introjs.com/)**, and **[Hopscotch](http://linkedin.github.io/hopscotch/)**. Choose your favorite one to use!

Example tour:

<img src="https://cdn2.hubspot.net/hubfs/100006/google_tour_3.gif" title="SeleniumBase Tour of Google" height="260"><br>


### Creating a new tour:

#### To create a tour utilizing the Shepherd JS Library, use one of the following:

``self.create_shepherd_tour()``

OR

``self.create_tour(theme="shepherd")``

You can pass a custom theme to change the look & feel of Shepherd tours. Valid themes for Shepherd Tours are ``dark``, ``light`` / ``arrows``, ``default``, ``square``, and ``square-dark``.

#### To create a tour utilizing the Bootstrap Tour Library, use one of the following:

``self.create_bootstrap_tour()``

OR

``self.create_tour(theme="bootstrap")``

#### To create a tour utilizing the Intro JS Library, use one of the following:

``self.create_introjs_tour()``

OR

``self.create_tour(theme="introjs")``

#### To create a tour utilizing the Hopscotch JS Library, use one of the following:

``self.create_hopscotch_tour()``

OR

``self.create_tour(theme="hopscotch")``

### Adding a step to a tour:

#### To add a tour step, use the following:

``self.add_tour_step(message, css_selector, title, alignment, theme)``

With the ``self.add_tour_step()`` method, you must first pass a message to display. You can then specify a web element to attach to (by using [CSS selectors](https://www.w3schools.com/cssref/css_selectors.asp)). If no element is specified, the tour step will tether to the top of the screen by default. You can also add an optional title above the message to display with the tour step, as well as change the theme for that step (Shepherd tours only), and even specify the alignment (which is the side of the element that you want the tour message to tether to).


### Playing a tour:

You can play a tour by calling:

``self.play_tour(interval)``

 If you specify an interval (optional), the tour will automatically walk through each step after that many seconds have passed.


All methods have the optional ``name`` argument, which is only needed if you're creating multiple tours at once. Then, when you're adding a step or playing a tour, SeleniumBase knows which tour you're referring too. You can avoid using the ``name`` arg for multiple tours if you play a tour before creating a new one.

### Here's an example of using SeleniumBase Tours:

```python
from seleniumbase import BaseCase

class MyTourClass(BaseCase):

    def test_google_tour(self):
        self.open('https://google.com')
        self.wait_for_element('input[title="Search"]')

        self.create_tour(theme="dark")
        self.add_tour_step(
            "Click to begin the Google Tour!", title="SeleniumBase Tours")
        self.add_tour_step(
            "Type in your search query here.", 'input[title="Search"]')
        self.play_tour()

        self.highlight_update_text('input[title="Search"]', "Google")
        self.wait_for_element('[role="listbox"]')  # Wait for autocomplete

        self.create_tour(theme="light")
        self.add_tour_step(
            "Then click here to search.", 'input[value="Google Search"]')
        self.add_tour_step(
            "Or press [ENTER] after typing a query here.", '[title="Search"]')
        self.play_tour()
```

#### This example was taken from [google_tour.py](https://github.com/seleniumbase/SeleniumBase/blob/master/examples/tour_examples/google_tour.py), which you can run from the ``examples/tour_examples`` folder with the following command:

```bash
pytest google_tour.py
```

### Exporting a Tour:

If you want to save the tour you created as a JavaScript file, use:

``self.export_tour()``

OR

``self.export_tour(name=None, filename="my_tour.js")``

(``name`` is optional unless you gave custom names to your tours when you created them. ``filename`` is the name of the file to save the JavaScript to.) Once you've exported your tour, you can use it outside of SeleniumBase. You can even copy the tour's JavaScript code to the Console of your web browser to play the tour from there (you need to be on the correct web page for it to work).
