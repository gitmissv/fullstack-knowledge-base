# FORMS IN ANGULAR

 - Template Driven
 - Reactive



## Template-Driven Form (HTML)

<form>
    <div id="user-data">
    <div class="form-group">
        <label for="username"> Username</label>
        <input
            type="text"
            id="username"
            class="form-control"
            ngModel
            name="username"
            required>
    </div>

**NOTE** *If email input ... add email after required w/ space*  required email

*also if email ...*
  - #email="ngModel">  [after required email]
  - <span class="help-block" *ngIf="!email.valid && email.touched">Please enter a valid email address!</span>


### Validate button to submit

<button
    class="btn btn-primary"
    type="submit"
    [disabled]="!xxx.valid">Submit</button>


### Add CSS style showing invalid

input.ng-invalid.ng-touched {
    border: 1px solid red;
}

**NOTE** *If you want to apply to eveything in the form; use form (add space before .ng....) - otherwise, use input or other class to target*

   - i.e.:  form .ng-invalid.ng-touched


_______________________

## Reactive Form (ts)

