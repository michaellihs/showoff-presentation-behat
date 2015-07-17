!SLIDE section_slide
# Custom Step Definitions

## How to write your own step definitions



!SLIDE code_slide
# Custom Step Definition in Gherkin

    @@@ gherkin
    Background:
      And I am in "desktop" layout



!SLIDE code_slide
# Missing Step Definition

    @@@ shell
    $ bin/behat

    --- FeatureContext has missing steps. \
        Define them with these snippets:

        /**
         * @Given I am in :arg1 layout
         */
        public function iAmInLayout($arg1)
        {
            throw new PendingException();
        }



!SLIDE code_slide
# Implement Step Definition

    @@@ php
    class ResponsiveContext extends RawMinkContext
       implements ContextInterface {

       /**
        * @When I am in :layout layout
        */
       public function resizeWindowLayout($layout) {
         $settings = $this->settings[$layout];
         $this->getSession()->getDriver()
            ->resizeWindow(
              $settings['width'],
              $settings['height'],
              'current'
            );
         return TRUE;
       }
    }



!SLIDE code_slide
# Add Context to behat.yaml

    @@@ yaml
    default:
	  contexts:
		-
		  PunktDe\ResponsiveContext
