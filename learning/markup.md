# Markup portfolio

## 1. Structure a site using semantic HTML to aid accessibility
  https://github.com/nataliarusu/a11y

## 2. Make a web page more readable for screen readers

## 3. Design a UI without relying solely on colour, so that we don’t exclude colour-blind users
  https://github.com/fac26/Natalia-Laura-Konstantina-Team/commit/1fb3c53de112ecb5f81829d8a76ab03e39247c30

## 4. Ensure our UI has sufficient colour contrast so that everyone can perceive it comfortably
  using Lighthouse developer tool on the browser 

## 5. Use various tools to check that a website meets accessibility criteria
  https://github.com/fac26/Natalia-Laura-Konstantina-Team/commit/8a22ce6a2014dd2122dd7bc495f57075b115ccd5

## 6. Ensure a website displays well on screens of different sizes

    @media screen and (max-width: 480px) {
      #team > * + * {
        max-width: 100%;
      }
      }
    @media screen and (max-width: 600px) {
     footer span {
      .slideshow-container {
        width: 100vw;
      }
      .team-member{
        flex-direction: column;
      }
    }
  

## 7. Use CSS media queries to ensure content is always presented effectively 
  https://github.com/fac26/Natalia-Laura-Konstantina-Team/commit/481f2566942267f8f1e2a690ada28e0aa3c65cb8

## 8. Demonstrate a mobile-first approach to designing a website with a great user experience
  https://github.com/fac26/Dominic_Natalia_http/blob/main/style.css
  
    #form-search-country input,
      .country-list {
        width: 70vw;
     }

    @media screen and (min-width: 600px) {
      #form-search-country input,
      .country-list {
        width: 40vw;
      }
    }
    

## 9. Create an attractive and accessible colour palette for a project
  https://github.com/nataliarusu/palette

## 10. Use CSS variables to apply repeated colours to HTML elements
  https://github.com/fac26/Natalia-Laura-Konstantina-Team/blob/main/style.css
  
    :root {
    --light-green: #52ab98;
    --dark-green: #155048;
    --main-link-hover: #7a2b52;
    }
