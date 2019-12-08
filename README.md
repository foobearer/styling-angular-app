# Styling Angular Application
Best practices and things to consider when styling Angular application

## 1. How styles work in angular

#### View Encapsulation

        none    : this will remove custom scope selector to el and css.
                : to enable none view encapsulation, you have to import "ViewEncapsulation" from @angular/core and set it to 
                "encapsulation: ViewEncapsulation.None" inside @Component.
                : it's best to use this when you want to set global styling for your app. It will be called first among all styles
                and it could be overwritten by the succeeding styles.
        emulated: is the default view encapsulation in ng app.
                : this adds unique ng host/content (custom scope) selector to each html el. within the encapsulated component.
        native  : this will not use ng custom scope selector but it will create Shadow root for CSS. Browsers that supports Shadow DOM 
                could only display shadow root selector. (e.i. Chrome)
                : "encapsulation: ViewEncapsulation.Emulated"

#### Emulated CSS Selectors
CSS Scoping Module: (pseudo classes)

        : :host - : host(.classname)
                  : this will apply to the root element in the component
        : :host-context - "host-context(.classname)
                  : this will look up the tree node within the component and adds few options to where to apply the styling.
        : /deep/ | >>> - this will look for the elements that are not implicitly define in the component then apply the styling. 
                  But it will apply the css globally and would affect other elements, so adding a pseudo class within >>> will 
                  lessen the probability of overriding styles in other components.

#### Adding Styles in Component

        : styles property - [``]
        : embedded        - <style></style>
        : linked          - <link rel="stylesheet" href="app/component-stylesheet-name.scss">
        : imported        - @import 'component-stylesheet-name.scss';
        : inline          - <div styles="color: red">
        : external        - styleUrls: ['component-stylesheet-name.scss']



## 2. Scalable, maintainable CSS/SCSS Architecture in Angular

        Global styles: 

                Browser resets
                Colors
                Typography
                Layout
                Media Queries
                Utilities

        Applying global styles:

                Class based systems
                Mixins & Variables


## 3. CSS Methodology - B.E.M. (Block__element--modifier) 

#### Ex. Traditional way

    <div class="main-header">
        <ul class="main-header__item"> 
            <li class="main-header__item-list
                       main-header__item-list--active"> List 1 </li>
            <li class="main-header__item-list"> List 2 </li>
            <li class="main-header__item-list"> List 3 </li>
        </ul>
    </div>

    block   : main-header
    element : main-header__item, main-header__item-list
    modifier: main-header__item-list--active

#### Ex. Angular way

    <div class="header">
        <ul class="item">
            <li class="item-list item-list--active"> List 1 </li>
            <li class="item-list"> List 2 </li>
            <li class="item-list"> List 3 </li>
        </ul>
    </div>

    block   : header
    element : item, item-list
    modifier: item-list--active

#### Ex. Using BEM with Sass

    .header {

        /* styles */

    }

    .__item {

        /* styles */

        .item-list {

            /* styles */

            &.--active {

                /* styles */

            }
        }
    }

    


#### Predictable Sizing with Relative Units
    unit to use : rem
    
    :host {
        font-size: 1rem;
    }

    .header {
        font-size: 1.5rem;
    }

## 4. Good Practices

    : keep specificity low
    : avoid styles overrides
    : use CSS Methodology
    : use class only to define styles
    : avoid using IDs as selector
