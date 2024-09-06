#  SignupNotes Vue Component

The `signupnotes/vue` package provides a Vue.js component to easily integrate SignupNotes forms into your Vue application.


## Installation

    npm install signupnotes/vue
    yarn add signupnotes/vue

## Usage

    import { SignupNotesForm } from '@signupnotes/signupnotes-vue'
	
    <SignupNotesForm
		class="h-full w-full"
		:values="{
			name:'John'
		}"
		:meta-data="{
			source:'web'
		}"
		form-id="yourFormId"
		@submit-data="handleSubmit"
		@step-change="handleStepChange"
		@loading="handleLoading"
		@loaded="handleLoaded"
	/>

## Props

-   **formId** (required): The unique ID of the form.
-   **values** (optional): Pre-fill form values as a record.
-   **meta-data** (optional): Additional metadata to send with the form.

## Events
-   **@submit-data**: Triggered when the form is successfully submitted. Returns form data.
-   **@step-change**: Triggered when the form step changes. Returns the current step number.
-   **@loading**: Triggered when the form starts loading. Returns a boolean indicating the loading state.
-   **@loaded**: Triggered when the form finishes loading. Returns a boolean indicating the loaded state.
