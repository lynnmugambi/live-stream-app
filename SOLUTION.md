
**How long did it take you to complete this assignment?**
4hrs

**What about this assignment did you find most challenging?**
Deciding how to sync the view between the display and selected options. Ended up passing classes that was very efficient. I tried to implement it by reusing the code as much as possible.

**What about this assignment did you find unclear?**
The figma mocks really helped to clear everything up. Thanks for including that.

**What challenges did you face that you did not expect?**
Definitely composing the modal was an unexpected challenge. It needed alot more elements and styling that the other components to achieve the look I was going for.

**Do you feel like this assignment has an appropriate level of difficulty?**
Yes

**Briefly explain your decisions to use tools, frameworks, and libraries like React, Vue, etc.**

*Vue 2*

This was my framework of choice and that I am most comfortable with. I especially enjoy developing with Vue because of its simplicity, comprehensive documentation and support with adjacent libraries.

*TailwindCSS*

Tailwind is a CSS utility framework. it relieved me from having to write loads of CSS and instead, I could use Tailwind directly in my HTML if needed. It also helped me style my HTML elements much faster. I especially like it because its lightweight as compared to other libraries like bootstrap. It is also easily customizable using the config.

**Did you make certain assumptions and decisions around the UI/UX? Please elaborate on your reasonings.**
*Modal*
- I added a close button and submit button to the modal. I found that this would help the user navigate the UI easily when the modal was open. The close button allows the user to exit the modal without affecting the current state, while the submit button, allows the user to submit the current selected options; with their options displayed on submission. I also added validation so the submit button is disabled when no option is selected.
- I also added selection indicators within the modal (A Teal Border around the selected option). This served as a visual aid for the user to show which option had been selected successfully.

*Look and Feel*
- I didn't actually end up calculating the screen sizes for the Video Feed (80% and 60%) from css (although it can be done); I used padding for easy configuration and an even look.
- As product of prioritization, I left out responsiveness; in the assumption that most our users will be on desktop. This can be added in the future if data shows increase in use of the product on smaller screens.
