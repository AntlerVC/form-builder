# Automation of filling AntlerVC/form-builder forms using playwright

Sample useage:

```javascript
const { chromium } = require('playwright');
const formFiller = require('.');

const formData = [
  {
    // rich text
    label: 'description',
    value: 'a random description',
  },
  {
    // text
    label: 'Unique page header (max. 100 characters)',
    value: 'a random page header',
  },
  {
    // text field (long text)
    label: 'Tell me more',
    value: 'bla bla blablabla',
  },
  {
    // single selector
    label: 'Who is the CEO of Antler?',
    value: 'Option 2',
  },
  {
    // multiple selector
    label: 'Who are Antler Engineering team members?',
    value: ['Option 2', 'Option 3'],
  },
  {
    // single selector with MultiSelect component
    label: 'ceo of facebook',
    value: 'Option 2',
  },
  {
    // checkbox
    label: 'I am not a robot',
    value: true,
  },
  {
    // radio
    label: 'Highest education level?',
    value: 'Option 4',
  },
  {
    // slider
    label: 'Your age',
    value: 5,
  },
  {
    // multiple text
    label: 'Previous employers',
    value: ['Antler', 'Antler Sydney', 'Antler Australia'],
  },
  {
    // color picker
    label: 'Preferred color for your Antler shirt?',
    value: '#ff00ff',
  },
  {
    // date selector
    label: 'Your birthday',
    value: '19701025', // format: "YYYYMMDD"
  },
  {
    // datetime selector
    label: 'book a time',
    value: '199010201050a', // format: "YYYYMMDDHHMM[a/p]"
  },
  {
    // error
    label: 'None existing label',
    value: '',
  },
];

async function main() {
  const browser = await chromium.launch({
    headless: false,
    slowMo: 0,
  });
  const page = await browser.newPage();
  await page.goto('http://localhost:1234');

  await formFiller(page, formData);
  await page.waitForTimeout(10000);
  // await page.waitForSelector(`//div[normalize-space(.)="Profile saved"]`);
  await browser.close();
}

main();
```
