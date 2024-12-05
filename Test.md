
# **Features for Pinterest Platform**

---

## **1. User Features**

---

### **1.1 Feature: User - Sign Up**

#### **Scenario: User signs up with email**

- **Given:**
  - The user is on the Pinterest sign-up page.
  
- **When:**
  - The user enters their email, password, and age.
  - The user clicks the "Sign Up" button.

- **Then:**
  - The user should be signed up successfully.
  - The user should be redirected to the Pinterest homepage.

```javascript
const chai = require('chai');
const expect = chai.expect;
const signUpPage = require('../pages/signUpPage');

describe('User - Sign Up', function () {
  it('should sign up the user successfully', function () {
    signUpPage.open();
    signUpPage.fillSignUpForm('user@example.com', 'securePassword123', 25);
    signUpPage.submitForm();
    expect(signUpPage.getWelcomeMessage()).to.include('Welcome to Pinterest');
    expect(browser.getUrl()).to.include('/home');
  });
});
```

---

### **1.2 Feature: User - Search Pins**

#### **Scenario: User searches for pins**

- **Given:**
  - The user is logged in.
  - The user is on the Pinterest homepage.

- **When:**
  - The user enters a search query in the search bar.
  - The user presses Enter or clicks the search icon.

- **Then:**
  - Relevant pins should be displayed.
  - The search term should appear in the search bar.

```javascript
const chai = require('chai');
const expect = chai.expect;
const homepage = require('../pages/homepage');

describe('User - Search Pins', function () {
  it('should display relevant pins for a search query', function () {
    homepage.open();
    homepage.searchPins('home decor');
    const displayedPins = homepage.getDisplayedPins();
    expect(displayedPins).to.not.be.empty;
    expect(homepage.getSearchBarValue()).to.equal('home decor');
  });
});
```

---

### **1.3 Feature: User - Save a Pin**

#### **Scenario: User saves a pin to a board**

- **Given:**
  - The user is logged in.
  - The user is viewing a pin.

- **When:**
  - The user clicks the "Save" button.
  - The user selects a board.

- **Then:**
  - The pin should be saved to the selected board.
  - A confirmation message should be displayed.

```javascript
const chai = require('chai');
const expect = chai.expect;
const pinPage = require('../pages/pinPage');
const boardPage = require('../pages/boardPage');

describe('User - Save a Pin', function () {
  it('should save the pin to the selected board', function () {
    pinPage.open('pin_id_123');
    pinPage.clickSaveButton();
    pinPage.selectBoard('My Favorites');
    expect(pinPage.getSaveConfirmation()).to.include('Saved to My Favorites');

    boardPage.open('My Favorites');
    expect(boardPage.getPins()).to.include('pin_id_123');
  });
});
```

---

### **1.4 Feature: User - Create a New Board**

#### **Scenario: User creates a new board**

- **Given:**
  - The user is logged in.
  - The user is on the Pinterest homepage.

- **When:**
  - The user clicks on "Create Board."
  - The user enters a board name and clicks "Create."

- **Then:**
  - The new board should be created.
  - The board should be visible in the user's profile.

```javascript
const chai = require('chai');
const expect = chai.expect;
const homepage = require('../pages/homepage');
const profilePage = require('../pages/profilePage');

describe('User - Create a New Board', function () {
  it('should create a new board successfully', function () {
    homepage.open();
    homepage.clickCreateBoard();
    homepage.fillBoardDetails('Travel Plans');
    homepage.submitBoardCreation();

    profilePage.open();
    const boards = profilePage.getUserBoards();
    expect(boards).to.include('Travel Plans');
  });
});
```

---

### **1.5 Feature: User - Follow a User**

#### **Scenario: User follows another user**

- **Given:**
  - The user is logged in.
  - The user is on another user's profile page.

- **When:**
  - The user clicks the "Follow" button.

- **Then:**
  - The user should be following the profile.
  - The "Follow" button should change to "Following."

```javascript
const chai = require('chai');
const expect = chai.expect;
const profilePage = require('../pages/profilePage');

describe('User - Follow a User', function () {
  it('should allow the user to follow another profile', function () {
    profilePage.open('user_id_456');
    profilePage.clickFollowButton();
    expect(profilePage.getFollowButtonText()).to.equal('Following');
  });
});
```

---

## **2. Creator Features**

---

### **2.1 Feature: Content Creator - Upload a Pin**

#### **Scenario: Content Creator uploads a new pin**

- **Given:**
  - The content creator is logged in.
  - The content creator is on the pin upload page.

- **When:**
  - The creator uploads an image.
  - The creator fills in the pin title, description, and destination link.
  - The creator clicks "Publish."

- **Then:**
  - The pin should be published successfully.
  - The pin should appear on the creator's profile.

```javascript
const chai = require('chai');
const expect = chai.expect;
const uploadPage = require('../pages/uploadPage');

describe('Content Creator - Upload a Pin', function () {
  it('should upload a new pin successfully', function () {
    uploadPage.open();
    uploadPage.uploadImage('pin.jpg');
    uploadPage.fillPinDetails('Delicious Pasta Recipe', 'Try this amazing pasta recipe!', 'https://example.com/recipe');
    uploadPage.submitPin();

    const successMessage = uploadPage.getSuccessMessage();
    expect(successMessage).to.equal('Your pin has been published!');
  });
});
```

---

### **2.2 Feature: Content Creator - Edit a Pin**

#### **Scenario: Content Creator edits an existing pin**

- **Given:**
  - The content creator is logged in.
  - The creator has already uploaded a pin.
  - The creator is on the pin details page.

- **When:**
  - The creator clicks "Edit."
  - The creator updates the pin's title or description.
  - The creator clicks "Save."

- **Then:**
  - The pin should be updated with the new details.

```javascript
const chai = require('chai');
const expect = chai.expect;
const pinPage = require('../pages/pinPage');

describe('Content Creator - Edit a Pin', function () {
  it('should update the pin details successfully', function () {
    pinPage.open('pin_id_123');
    pinPage.clickEditButton();
    pinPage.updateDetails('New Title', 'Updated description.');
    pinPage.clickSaveButton();

    const updatedDetails = pinPage.getPinDetails();
    expect(updatedDetails.title).to.equal('New Title');
    expect(updatedDetails.description).to.equal('Updated description.');
  });
});
```

---

### **2.3 Feature: Content Creator - View Analytics**

#### **Scenario: Content Creator views pin analytics**

- **Given:**
  - The content creator is logged in.
  - The creator is on the analytics page for a pin.

- **When:**
  - The creator opens the analytics page.

- **Then:**
  - The creator should see metrics like impressions, saves, and link clicks.

```javascript
const chai = require('chai');
const expect = chai.expect;
const analyticsPage = require('../pages/analyticsPage');

describe('Content Creator - View Analytics', function () {
  it('should display analytics for a pin', function () {
    analyticsPage.open('pin_id_123');
    const metrics = analyticsPage.getMetrics();
    expect(metrics).to.have.property('impressions').that.is.a('number');
    expect(metrics).to.have.property('saves').that.is.a('number');
    expect(metrics).to.have.property('clicks').that.is.a('number');
  });
});
```

---

## **3. Pinterest Platform Features**

---

### **3.1 Feature: Home Feed Personalization**

#### **Scenario: User sees personalized home feed**

- **Given:**
  - The user is logged in.
  - The user has interacted with several pins.

- **When:**
  - The user visits the home feed.

- **Then:**
  - The home feed should display pins relevant to the user's interests.

---
