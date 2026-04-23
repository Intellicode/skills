# Accessible Component Patterns

Reference for building common UI components accessibly, inspired by GOV.UK Design System patterns.

## Form Input with Label, Hint, and Error

Always associate labels explicitly. Group hints and errors with `aria-describedby`.

```html
<div class="form-group form-group--error">
  <label class="label" for="email">
    Email address
  </label>
  <div id="email-hint" class="hint">
    We will only use this to send you a confirmation
  </div>
  <p id="email-error" class="error-message">
    <span class="visually-hidden">Error:</span> Enter an email address in the correct format, like name@example.com
  </p>
  <input class="input input--error" id="email" name="email" type="email"
         aria-describedby="email-hint email-error" autocomplete="email">
</div>
```

## Error Summary

Display at top of form. Link each error to its field. Programmatically focus on page load.

```html
<div class="error-summary" role="alert" tabindex="-1" aria-labelledby="error-summary-title">
  <h2 class="error-summary__title" id="error-summary-title">
    There is a problem
  </h2>
  <ul class="error-summary__list">
    <li>
      <a href="#email">Enter an email address in the correct format</a>
    </li>
  </ul>
</div>
```

Focus on load:
```js
const errorSummary = document.querySelector('.error-summary');
if (errorSummary) errorSummary.focus();
```

## Fieldset with Legend

Group related inputs. The legend becomes the audible label for the group.

```html
<fieldset class="form-group">
  <legend class="label">
    Have you changed your name?
  </legend>
  <div class="hint" id="changed-name-hint">
    This includes changing your last name or spelling your name differently.
  </div>
  <div class="radios">
    <div class="radios__item">
      <input class="radios__input" id="changed-name-yes" name="changed-name" type="radio" value="yes" aria-describedby="changed-name-hint">
      <label class="label radios__label" for="changed-name-yes">Yes</label>
    </div>
    <div class="radios__item">
      <input class="radios__input" id="changed-name-no" name="changed-name" type="radio" value="no" aria-describedby="changed-name-hint">
      <label class="label radios__label" for="changed-name-no">No</label>
    </div>
  </div>
</fieldset>
```

## Checkboxes

```html
<div class="checkboxes">
  <div class="checkboxes__item">
    <input class="checkboxes__input" id="waste-animal" name="waste" type="checkbox" value="animal">
    <label class="label checkboxes__label" for="waste-animal">Waste from animal carcasses</label>
  </div>
</div>
```

## Date Input

Use three separate fields with a single label, or a `fieldset` with `legend`. Never use `type="date"` (inconsistent screen reader support). Use `inputmode="numeric"` for on-screen numeric keyboards.

```html
<fieldset class="form-group">
  <legend class="label">When was your passport issued?</legend>
  <div class="hint" id="passport-issued-hint">For example, 27 3 2007</div>
  <div class="date-input">
    <div class="date-input__item">
      <label class="label" for="passport-issued-day">Day</label>
      <input class="input" id="passport-issued-day" name="passport-issued-day" type="text" inputmode="numeric" pattern="[0-9]*">
    </div>
    <div class="date-input__item">
      <label class="label" for="passport-issued-month">Month</label>
      <input class="input" id="passport-issued-month" name="passport-issued-month" type="text" inputmode="numeric" pattern="[0-9]*">
    </div>
    <div class="date-input__item">
      <label class="label" for="passport-issued-year">Year</label>
      <input class="input" id="passport-issued-year" name="passport-issued-year" type="text" inputmode="numeric" pattern="[0-9]*">
    </div>
  </div>
</fieldset>
```

## Select (Drop-down)

Use sparingly. If the list is short, use radio buttons instead (all options visible without interaction).

```html
<div class="form-group">
  <label class="label" for="sort">Sort by</label>
  <select class="input" id="sort" name="sort">
    <option value="published">Recently published</option>
    <option value="updated">Recently updated</option>
    <option value="views">Most views</option>
  </select>
</div>
```

## Button

```html
<button type="submit" class="button" data-module="button">
  Save and continue
</button>
```

For disabled buttons, avoid `disabled` attribute if user needs to know why. Instead, validate on submit and show errors.

## Details / Expandable Content

```html
<details class="details">
  <summary class="details__summary">
    <span class="details__summary-text">Help with nationality</span>
  </summary>
  <div class="details__text">
    <p class="body-text">We need to know your nationality so we can work out which elections you are entitled to vote in.</p>
  </div>
</details>
```

## Notification Banner

```html
<div class="notification-banner" role="region" aria-labelledby="notification-banner-title" data-module="notification-banner">
  <div class="notification-banner__header">
    <h2 class="notification-banner__title" id="notification-banner-title">Important</h2>
  </div>
  <div class="notification-banner__content">
    <p class="notification-banner__heading">You have 7 days left to send your application.</p>
  </div>
</div>
```

For success banners, use `role="alert"` to announce immediately:
```html
<div class="notification-banner notification-banner--success" role="alert" aria-labelledby="success-title">
  ...
</div>
```

## Table

Always use `<th>` for headers with `scope="col"` or `scope="row"`.

```html
<table class="table">
  <thead>
    <tr>
      <th scope="col" class="table__header">Month</th>
      <th scope="col" class="table__header">Rate for vehicles</th>
      <th scope="col" class="table__header">Rate for bicycles</th>
    </tr>
  </thead>
  <tbody>
    <tr class="table__row">
      <th scope="row" class="table__header">January</th>
      <td class="table__cell">£165</td>
      <td class="table__cell">£85</td>
    </tr>
  </tbody>
</table>
```

For complex tables, use `id` and `headers` attributes to associate data cells with headers.

## Pagination

```html
<nav class="pagination" role="navigation" aria-label="results">
  <div class="pagination__prev">
    <a class="pagination__link" href="#" rel="prev">
      <span class="pagination__link-title">Previous</span>
      <span class="visually-hidden">:</span>
      <span class="pagination__link-label">1 of 5</span>
    </a>
  </div>
  <ul class="pagination__list">
    <li class="pagination__item"><a class="pagination__link" href="#" aria-label="Page 1">1</a></li>
    <li class="pagination__item pagination__item--current" aria-current="page" aria-label="Page 2, current page">2</li>
    <li class="pagination__item"><a class="pagination__link" href="#" aria-label="Page 3">3</a></li>
  </ul>
  <div class="pagination__next">
    <a class="pagination__link" href="#" rel="next">
      <span class="pagination__link-title">Next</span>
      <span class="visually-hidden">:</span>
      <span class="pagination__link-label">3 of 5</span>
    </a>
  </div>
</nav>
```

## Warning Text

```html
<div class="warning-text">
  <span class="warning-text__icon" aria-hidden="true">!</span>
  <strong class="warning-text__text">
    <span class="warning-text__assistive">Warning</span>
    You can be fined up to £5,000 if you do not register.
  </strong>
</div>
```

## Inset Text

```html
<div class="inset-text">
  <p class="body-text">It can take up to 8 weeks to register a lasting power of attorney if there are no mistakes in the application.</p>
</div>
```

## Task List Pattern

Shows users what they need to do to complete a transaction.

```html
<ol class="task-list">
  <li>
    <h2 class="task-list__section"><span class="task-list__section-number">1. </span>Check before you start</h2>
    <ul class="task-list__items">
      <li class="task-list__item">
        <span class="task-list__task-name">
          <a href="#" aria-describedby="eligibility-status">Check eligibility</a>
        </span>
        <strong class="tag" id="eligibility-status">Completed</strong>
      </li>
    </ul>
  </li>
</ol>
```
