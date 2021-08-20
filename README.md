Title: Inlining CSS from our react display component library to improve scores

We at [Quintype](https://www.quintype.com/) have built a [react framework](https://developers.quintype.com/malibu/) which does isomorphic rendering. We also have a component library called [Arrow](https://www.npmjs.com/package/@quintype/arrow) which provides pre-styled customizable react components - for example some *rows* from [here](https://developers.quintype.com/quintype-node-arrow/?path=/story/rows-four-col-grid--default) are being used [here](https://malibu-advanced-web.quintype.io/).

**The problem:**
On integrating Arrow components in our app, the pages were having quite poor web vitals. One of the reasons being the component CSS wasn't being inlined during SSR

**Solution:**
Inline some CSS. We don't know which components would be used above the fold at build time, since that can be customized from the CMS. However we do know this at runtime - the CMS sends it as a config. So we generated seperate CSS files for every library component, created seperate bundles for every *row* component in our app and changed the SSR logic to inline the styles of the 1st *row* component.
This isn't really *critical css* but it improved our scores - CLS has become close to 0
