
# Advanced Requirements Engineering BDD Demo

RE BDD acceptance-test scenario results for seamless E-commerce art gallery web app using Spring Boot.

Cucumber test results are generated from a workflow run on an advanced University of Auckland project.

Advanced Requirements Engineering project, Group 1 members:
* Fuki Babasaki
* James Coppard
* Adam Ross
* Berverley Sun 
* Valerio Terragni

> Note: course/project is completed before ChatGPT and other Gen-AI models have been publicly available.

## Test Results

| Scenario Status | Count |
|---|---:|
| Passed | 91 |
| Failed | 0 |
| Skipped | 0 |

```gherkin
Feature: Purchasing Artwork
------------------

Scenario: [PASS] Successful buy now artwork

  Given I visit a buy now "Moonlight" page
  And The purchase amount for "Moonlight" is the 100.0
  When I select the buy now button
  And I complete the payment
  Then I should see a message "Success!"
  And I should no longer be able to purchase the artwork
  And I should see the "Moonlight" purchase in my profile

Scenario: [PASS] Successful buy now artwork

  Given I visit a buy now "Imagination" page
  And The purchase amount for "Imagination" is the 50.0
  When I select the buy now button
  And I complete the payment
  Then I should see a message "Success!"
  And I should no longer be able to purchase the artwork
  And I should see the "Imagination" purchase in my profile

Scenario: [PASS] Unsuccessful buy now artwork

  Given I visit a buy now "Moonlight" page
  And The purchase amount for "Moonlight" is the 100.0
  When I select the buy now button
  And I cancel the payment
  Then I should see an error message "Try Again"
  And I should be able to purchase the buy now artwork
  And The purchase amount for "Moonlight" is the 100.0
  And I should not see the "Moonlight" purchase in my profile

Scenario: [PASS] Unsuccessful buy now artwork

  Given I visit a buy now "Imagination" page
  And The purchase amount for "Imagination" is the 50.0
  When I select the buy now button
  And I cancel the payment
  Then I should see an error message "Try Again"
  And I should be able to purchase the buy now artwork
  And The purchase amount for "Imagination" is the 50.0
  And I should not see the "Imagination" purchase in my profile

Scenario: [PASS] Successful auction artwork bid

  Given I visit an auction "AuctionWithoutBid" page
  And The current bid for "AuctionWithoutBid" is 100.0
  When I enter 102.0 as a new bid amount
  And I select the bid button
  Then The current bid for "AuctionWithoutBid" is 102.0
  And I should see the bid for "AuctionWithoutBid" on my profile
  And I should not see the "AuctionWithoutBid" purchase in my profile

Scenario: [PASS] Successful auction artwork bid

  Given I visit an auction "AuctionWithBid" page
  And The current bid for "AuctionWithBid" is 1.0
  When I enter 2.0 as a new bid amount
  And I select the bid button
  Then The current bid for "AuctionWithBid" is 2.0
  And I should see the bid for "AuctionWithBid" on my profile
  And I should not see the "AuctionWithBid" purchase in my profile

Scenario: [PASS] Unsuccessful auction artwork bid too low

  Given I visit an auction "AuctionWithoutBid" page
  And The current bid for "AuctionWithoutBid" is 100.0
  When I enter 99.0 as a new bid amount
  And I select the bid button
  Then The current bid for "AuctionWithoutBid" is 100.0
  And I should see an error message "Bid must be greater than the current bid in increments of $1"
  And I should not see the bid for "AuctionWithoutBid" on my profile
  And I should not see the "AuctionWithoutBid" purchase in my profile

Scenario: [PASS] Unsuccessful auction artwork bid too low

  Given I visit an auction "AuctionWithBid" page
  And The current bid for "AuctionWithBid" is 1.0
  When I enter 0.0 as a new bid amount
  And I select the bid button
  Then The current bid for "AuctionWithBid" is 1.0
  And I should see an error message "Bid must be greater than the current bid in increments of $1"
  And I should not see the bid for "AuctionWithBid" on my profile
  And I should not see the "AuctionWithBid" purchase in my profile

Scenario: [PASS] Unsuccessful auction artwork bid not increment of 1

  Given I visit an auction "AuctionWithoutBid" page
  And The current bid for "AuctionWithoutBid" is 100.0
  When I enter 1000.9 as a new bid amount
  And I select the bid button
  Then The current bid for "AuctionWithoutBid" is 100.0
  And I should see an error message "Bid must be greater than the current bid in increments of $1"
  And I should not see the bid for "AuctionWithoutBid" on my profile
  And I should not see the "AuctionWithoutBid" purchase in my profile

Scenario: [PASS] Unsuccessful auction artwork bid not increment of 1

  Given I visit an auction "AuctionWithBid" page
  And The current bid for "AuctionWithBid" is 1.0
  When I enter 2.1 as a new bid amount
  And I select the bid button
  Then The current bid for "AuctionWithBid" is 1.0
  And I should see an error message "Bid must be greater than the current bid in increments of $1"
  And I should not see the bid for "AuctionWithBid" on my profile
  And I should not see the "AuctionWithBid" purchase in my profile

Scenario: [PASS] Successful auction artwork winning bid purchase

  Given I visit an auction "AuctionWonForStartingPrice" page I have the winning bid for
  And The purchase amount for auction "AuctionWonForStartingPrice" is the 1.0
  When I select the Complete Purchase button
  And I complete the payment
  Then I should see a message "Success!"
  And I should no longer be able to purchase the artwork
  And I should see the "AuctionWonForStartingPrice" purchase in my profile

Scenario: [PASS] Successful auction artwork winning bid purchase

  Given I visit an auction "AuctionWonForHighestBidPrice" page I have the winning bid for
  And The purchase amount for auction "AuctionWonForHighestBidPrice" is the 2.0
  When I select the Complete Purchase button
  And I complete the payment
  Then I should see a message "Success!"
  And I should no longer be able to purchase the artwork
  And I should see the "AuctionWonForHighestBidPrice" purchase in my profile

Scenario: [PASS] Unsuccessful auction artwork winning bid purchase

  Given I visit an auction "AuctionWonForStartingPrice" page I have the winning bid for
  And The purchase amount for auction "AuctionWonForStartingPrice" is the 1.0
  When I select the Complete Purchase button
  And I cancel the payment
  Then I should see an error message "Try Again"
  And I should be able to purchase the auction artwork
  And The purchase amount for auction "AuctionWonForStartingPrice" is the 1.0
  And I should not see the "AuctionWonForStartingPrice" purchase in my profile

Scenario: [PASS] Unsuccessful auction artwork winning bid purchase

  Given I visit an auction "AuctionWonForHighestBidPrice" page I have the winning bid for
  And The purchase amount for auction "AuctionWonForHighestBidPrice" is the 2.0
  When I select the Complete Purchase button
  And I cancel the payment
  Then I should see an error message "Try Again"
  And I should be able to purchase the auction artwork
  And The purchase amount for auction "AuctionWonForHighestBidPrice" is the 2.0
  And I should not see the "AuctionWonForHighestBidPrice" purchase in my profile

Scenario: [PASS] Successful auction artwork bid equal to start price

  Given I visit an auction "AuctionWithoutBid" page
  And The start price amount for "AuctionWithoutBid" is 100.0
  When I enter 100.0 as a new bid amount
  And I select the bid button
  Then The current bid for "AuctionWithoutBid" is 100.0
  And I should see the bid for "AuctionWithoutBid" on my profile
  And I should not see the "AuctionWithoutBid" purchase in my profile

Scenario: [PASS] Unsuccessful auction artwork bid before start datetime

  Given I visit an auction "AuctionNotStarted" page
  And The current bid for "AuctionNotStarted" is 300.0
  When I enter 1000.0 as a new bid amount
  And I select the bid button
  Then The current bid for "AuctionNotStarted" is 300.0
  And I should see an error message "Auction has not started"
  And I should not see the bid for "AuctionNotStarted" on my profile
  And I should not see the "AuctionNotStarted" purchase in my profile

Scenario: [PASS] Unsuccessful auction artwork bid after end datetime

  Given I visit an auction "AuctionClosed" page
  And The current bid for "AuctionClosed" is 50.0
  When I enter 60.0 as a new bid amount
  And I select the bid button
  Then The current bid for "AuctionClosed" is 50.0
  And I should see an error message "Auction has closed"
  And I should not see the bid for "AuctionClosed" on my profile
  And I should not see the "AuctionClosed" purchase in my profile

Scenario: [PASS] Unsuccessful auction artwork bid equal to current bid price

  Given I visit an auction "AuctionWithBid" page
  And The current bid amount for "AuctionWithBid" is 1.0
  When I enter 1.0 as a new bid amount
  And I select the bid button
  Then The current bid amount for "AuctionWithBid" is 1.0
  And I should see an error message "Bid must be greater than the current bid in increments of $1"
  And I should not see the bid for "AuctionWithBid" on my profile
  And I should not see the "AuctionWithBid" purchase in my profile


Feature: Admin Editing
-------------

Scenario: [PASS] Edit artwork information

  When I edit description of 1th artwork in the list to "This ancient visual tradition is surveyed through 118 captivating icons."
  Then I should see the updated 1th artwork description "This ancient visual tradition is surveyed through 118 captivating icons."

Scenario: [PASS] Edit artwork information

  When I edit description of 2th artwork in the list to "the seat of Eastern Christianity"
  Then I should see the updated 2th artwork description "the seat of Eastern Christianity"

Scenario: [PASS] Edit artwork information

  When I edit description of 4th artwork in the list to "Constructed entirely from stainless-steel tube."
  Then I should see the updated 4th artwork description "Constructed entirely from stainless-steel tube."

Scenario: [PASS] Edit description with more than 200 words

  When I edit description with 201 words
  Then I should be informed it exceeded the word limit
  And I should see no changes

Scenario: [PASS] Edit artwork that has already been sold

  When I edit artwork that has already been sold
  Then I should be informed it has been sold
  And I should see no changes

Scenario: [PASS] Edit auction that has already started

  When I edit auction that has already started
  Then I should be informed it has started
  And I should see no changes

Scenario: [PASS] List new art

  When I list an artwork with "New Art" and "Entirely new art."
  Then I should see the new listed artwork with "New Art"

Scenario: [PASS] List new art

  When I list an artwork with "An Arrangement for 5 Rooms" and "Lee picks up the signature handrail of the Gallery architecture"
  Then I should see the new listed artwork with "An Arrangement for 5 Rooms"

Scenario: [PASS] Edit new listed art

  When I list an artwork with "Love is in the Bin" and "to be confirmed"
  And I edit the new listed artwork with "The painting is an adaptation of Banksy's 2002 mural Girl with Balloon"
  Then I should see the description of the listed artwork updated to "The painting is an adaptation of Banksy's 2002 mural Girl with Balloon"

Scenario: [PASS] Edit new listed art

  When I list an artwork with "Girl with Balloon" and "undefined"
  And I edit the new listed artwork with "2002-started London series of stencil murals by the graffiti artist Banksy"
  Then I should see the description of the listed artwork updated to "2002-started London series of stencil murals by the graffiti artist Banksy"

Scenario: [PASS] List new art with duplicate title

  Given An artwork with "Duplicate Title" is listed
  When I list an artwork with "Duplicate Title"
  Then I should be informed it has duplicate title

Scenario: [PASS] List new art with duplicate title

  Given An artwork with "Cucumber" is listed
  When I list an artwork with "Cucumber"
  Then I should be informed it has duplicate title


Feature: Admin Permission
----------------

Scenario: [PASS] Successful login

  When I log in with a valid "admin1" and "password" as an admin
  Then I should see the admin page with a message "Welcome admin1"

Scenario: [PASS] Successful login

  When I log in with a valid "admin2" and "pa33w0rd" as an admin
  Then I should see the admin page with a message "Welcome admin2"

Scenario: [PASS] Unsuccessful login

  When I log in with an invalid "admin1" and/or "pa33w0rd" as an admin
  Then I should get an error "Invalid password"

Scenario: [PASS] Unsuccessful login

  When I log in with an invalid "admin" and/or "password" as an admin
  Then I should get an error "Username does not exist"

Scenario: [PASS] Unsuccessful login

  When I log in with an invalid "tom" and/or "12345" as an admin
  Then I should get an error "Username does not exist"


Feature: Gallery Payment
---------------

Scenario: [PASS] Place bid with payment method

  Given I am logged in as a user with a payment method
  And I visit an auction page
  And I attempt to place a bid
  Then I should not get a bid error

Scenario: [PASS] Place bid with no payment method

  Given I am logged in as a user with no payment method
  And I visit an auction page
  And I attempt to place a bid
  Then I should get an error message "You need to have at least one payment method registered to bid"

Scenario: [PASS] Add payment info

  Given I am logged in as a user with no payment method
  When I add payment info with "1111111111111111" "12/27" "111"
  Then I should see payment info with "**** 1111" "12/27" on my profile

Scenario: [PASS] Add invalid payment info

  Given I am logged in as a user with no payment method
  When I add payment info with "1111111111111111" "" "111"
  Then I should get a card invalid message "Expiry is invalid"

Scenario: [PASS] Add invalid payment info

  Given I am logged in as a user with no payment method
  When I add payment info with "" "12/27" "111"
  Then I should get a card invalid message "Card number is invalid"

Scenario: [PASS] Add invalid payment info

  Given I am logged in as a user with no payment method
  When I add payment info with "1111111111111111" "12/27" ""
  Then I should get a card invalid message "Cvc is invalid"

Scenario: [PASS] Add invalid payment info

  Given I am logged in as a user with no payment method
  When I add payment info with "1111111111111111" "01/25" "111"
  Then I should get a card invalid message "Card is expired"

Scenario: [PASS] Buy artwork successful purchase

  Given I am logged in as a user with a payment method
  And I visit a buy now page
  When I click buy
  And I complete the payment
  Then I should get a success message "Success!"

Scenario: [PASS] Buy artwork failed purchase

  Given I am logged in as a user with a payment method
  And I visit a buy now page
  When I click buy
  And I cancel the payment
  Then I should get an error message "Try Again"


Feature: Information Sensitivity
-----------------------

Scenario: [PASS] Successful customer login

  When I enter "user1" in the username input field
  And I enter "password1" in the password input field
  And I press the login button
  Then I should see my profile greeting me with "User 1" and "user1" displayed

Scenario: [PASS] Successful customer login

  When I enter "user2" in the username input field
  And I enter "password2" in the password input field
  And I press the login button
  Then I should see my profile greeting me with "User 2" and "user2" displayed

Scenario: [PASS] Unsuccessful customer login

  When I enter "user1" in the username input field
  And I enter "wrongpassword1" in the password input field
  And I press the login button
  Then I should see an error message: "Invalid credentials"

Scenario: [PASS] Unsuccessful customer login

  When I enter "user2" in the username input field
  And I enter "wrongpassword2" in the password input field
  And I press the login button
  Then I should see an error message: "Invalid credentials"

Scenario: [PASS] View history

  When I enter "user1" in the username input field
  And I enter "password1" in the password input field
  And I press the login button
  Then I should see "Moonlight" and "Sunlight" in my purchase history
  And I should see "Still Life" in my current bids

Scenario: [PASS] View history

  When I enter "user2" in the username input field
  And I enter "password2" in the password input field
  And I press the login button
  Then I should see "Frog" and "Paper" in my purchase history
  And I should see "Red on Blue" in my current bids

Scenario: [PASS] View payment methods

  When I enter "user1" in the username input field
  And I enter "password1" in the password input field
  And I press the login button
  Then I should see "**** 1234" and "12/23"
  And "**** 9876" and "09/24" in my saved cards

Scenario: [PASS] View payment methods

  When I enter "user2" in the username input field
  And I enter "password2" in the password input field
  And I press the login button
  Then I should see "**** 2468" and "24/24"
  And "**** 1357" and "11/22" in my saved cards

Scenario: [PASS] Change password

  When I click the change password button
  And I enter "user1" in the current username input field
  And I enter "password1" in the current password input field
  And I enter "newPassword1" in the new password input field
  And I click the confirm new password button
  Then I should see the message "Successful!"

Scenario: [PASS] Change password

  When I click the change password button
  And I enter "user2" in the current username input field
  And I enter "password2" in the current password input field
  And I enter "newPassword2" in the new password input field
  And I click the confirm new password button
  Then I should see the message "Successful!"

Scenario: [PASS] Change password

  When I click the change password button
  And I enter "user2" in the current username input field
  And I enter "wrongpassword1" in the current password input field
  And I enter "newPassword2" in the new password input field
  And I click the confirm new password button
  Then I should see the message "Invalid credentials"

Scenario: [PASS] Change password

  When I click the change password button
  And I enter "user2" in the current username input field
  And I enter "wrongpassword2" in the current password input field
  And I enter "newPassword2" in the new password input field
  And I click the confirm new password button
  Then I should see the message "Invalid credentials"


Feature: Seeing artwork
--------------

Scenario: [PASS] Browse all artwork

  Given the gallery sells artworks titled: "My art", "Your art", and "Our art"
  When I click the browse all artwork link
  Then I should see "My art", "Your art", and "Our art" displayed on the page

Scenario: [PASS] Browse all artwork

  Given the gallery sells artworks titled: "Whose art?", "Their art", and "Her art"
  When I click the browse all artwork link
  Then I should see "Whose art?", "Their art", and "Her art" displayed on the page

Scenario: [PASS] Browse all artwork

  Given the gallery sells artworks titled: "Some art", "New art", and "Old art"
  When I click the browse all artwork link
  Then I should see "Some art", "New art", and "Old art" displayed on the page

Scenario: [PASS] Browse all artwork

  Given the gallery sells artworks titled: "His art", "Cool art", and "Pretty art"
  When I click the browse all artwork link
  Then I should see "His art", "Cool art", and "Pretty art" displayed on the page

Scenario: [PASS] Browse by category

  Given the gallery has "Sculpture" and "Auction" categories
  When I look at the page
  Then I should see a browse by categories section
  And there should be "Sculpture" and "Auction" listed

Scenario: [PASS] Browse by category

  Given the gallery has "Picasso" and "Buy Now" categories
  When I look at the page
  Then I should see a browse by categories section
  And there should be "Picasso" and "Buy Now" listed

Scenario: [PASS] Browse by category

  Given the gallery has "Vincent van Gogh" and "Painting" categories
  When I look at the page
  Then I should see a browse by categories section
  And there should be "Vincent van Gogh" and "Painting" listed

Scenario: [PASS] Browse by category

  Given the gallery has "Buy Now" and "Print" categories
  When I look at the page
  Then I should see a browse by categories section
  And there should be "Buy Now" and "Print" listed

Scenario: [PASS] Click on category

  Given the gallery has auctioned art, buy now art, painting, print, sculpture, van Gogh, and Picasso categories
  And there are 4 artworks in "Auction"
  When I look at the page
  And I click on the "Auction" link
  Then I should see 4 artworks displayed

Scenario: [PASS] Click on category

  Given the gallery has auctioned art, buy now art, painting, print, sculpture, van Gogh, and Picasso categories
  And there are 3 artworks in "Buy Now"
  When I look at the page
  And I click on the "Buy Now" link
  Then I should see 3 artworks displayed

Scenario: [PASS] Click on category

  Given the gallery has auctioned art, buy now art, painting, print, sculpture, van Gogh, and Picasso categories
  And there are 6 artworks in "Painting"
  When I look at the page
  And I click on the "Painting" link
  Then I should see 6 artworks displayed

Scenario: [PASS] Click on category

  Given the gallery has auctioned art, buy now art, painting, print, sculpture, van Gogh, and Picasso categories
  And there are 1 artworks in "Print"
  When I look at the page
  And I click on the "Print" link
  Then I should see 1 artworks displayed

Scenario: [PASS] Click on category

  Given the gallery has auctioned art, buy now art, painting, print, sculpture, van Gogh, and Picasso categories
  And there are 7 artworks in "Sculpture"
  When I look at the page
  And I click on the "Sculpture" link
  Then I should see 7 artworks displayed

Scenario: [PASS] Click on category

  Given the gallery has auctioned art, buy now art, painting, print, sculpture, van Gogh, and Picasso categories
  And there are 3 artworks in "Vincent van Gogh"
  When I look at the page
  And I click on the "Vincent van Gogh" link
  Then I should see 3 artworks displayed

Scenario: [PASS] Click on category

  Given the gallery has auctioned art, buy now art, painting, print, sculpture, van Gogh, and Picasso categories
  And there are 4 artworks in "Picasso"
  When I look at the page
  And I click on the "Picasso" link
  Then I should see 4 artworks displayed

Scenario: [PASS] Pagination

  Given the gallery sells 4 artworks
  When I click the browse all artwork link
  Then I should see links to 1 pages
  And there should be 4 on each page except the last page
  And there should be 4 on the last page

Scenario: [PASS] Pagination

  Given the gallery sells 15 artworks
  When I click the browse all artwork link
  Then I should see links to 2 pages
  And there should be 10 on each page except the last page
  And there should be 5 on the last page

Scenario: [PASS] Pagination

  Given the gallery sells 80 artworks
  When I click the browse all artwork link
  Then I should see links to 8 pages
  And there should be 10 on each page except the last page
  And there should be 10 on the last page

Scenario: [PASS] Access nonexistent page

  Given the gallery sells 4 artworks
  When I try to access page 2
  Then I should be notified the page doesn't exist with: "No artworks found on page 2"

Scenario: [PASS] Access nonexistent page

  Given the gallery sells 15 artworks
  When I try to access page 4
  Then I should be notified the page doesn't exist with: "No artworks found on page 4"

Scenario: [PASS] Access nonexistent page

  Given the gallery sells 80 artworks
  When I try to access page 9
  Then I should be notified the page doesn't exist with: "No artworks found on page 9"

Scenario: [PASS] Search artwork

  Given the gallery sells 5 artworks with "search" in its information
  And 2 without it
  When I search for "search"
  Then I should see the 5 artworks with the search term in the results

Scenario: [PASS] Search artwork

  Given the gallery sells 3 artworks with "orange" in its information
  And 7 without it
  When I search for "orange"
  Then I should see the 3 artworks with the search term in the results

Scenario: [PASS] Search artwork

  Given the gallery sells 9 artworks with "person" in its information
  And 3 without it
  When I search for "person"
  Then I should see the 9 artworks with the search term in the results

Scenario: [PASS] Search artwork order

  Given the gallery sells 5 artworks with "peach" in its information
  When I search for "peach"
  Then I should see 5 artworks sorted by relevancy

Scenario: [PASS] Search artwork order

  Given the gallery sells 9 artworks with "hello" in its information
  When I search for "hello"
  Then I should see 9 artworks sorted by relevancy

Scenario: [PASS] Search artwork order

  Given the gallery sells 7 artworks with "something" in its information
  When I search for "something"
  Then I should see 7 artworks sorted by relevancy

Scenario: [PASS] View buy now art

  When I browse to artwork #0
  Then I should see "Moonlight", "Han Solo", "Moonlight is a new artwork, guaranteed to be loved by all.", "PAINTING", "$100.0", and an image

Scenario: [PASS] View buy now art

  When I browse to artwork #1
  Then I should see "Motion of Wonder", "Luke Skywalker", "An adventurer's dream.", "PRINT", "$200.0", and an image

Scenario: [PASS] View auction art

  When I browse to artwork #4
  Then I should see "AuctionNotStarted", "Artist 1", "Description 1", "SCULPTURE", "$300.0", "07-09-2026 09:00", "08-09-2026 17:00", and an image

Scenario: [PASS] View auction art

  When I browse to artwork #5
  Then I should see "AuctionClosed", "Artist 2", "Description 2", "PAINTING", "$50.0", "04-09-2026 15:30", "05-09-2026 19:30", and an image


Feature: Shipping
--------

Scenario: [PASS] Show shipping cost

  Given I am logged in as a user with a payment method
  And I visit a buy now page
  And I have entered my country "NZ"
  When I click calculate shipping cost
  Then I can see the shipping cost "6.5"

Scenario: [PASS] Show shipping cost

  Given I am logged in as a user with a payment method
  And I visit a buy now page
  And I have entered my country "USA"
  When I click calculate shipping cost
  Then I can see the shipping cost "50.0"

Scenario: [PASS] See total cost of purchase

  Given I am logged in as a user with a payment method
  And I visit a buy now page
  And I have entered my country "NZ"
  And I click calculate shipping cost
  When I click buy
  Then I can see the total cost "106.5"

Scenario: [PASS] See total cost of purchase

  Given I am logged in as a user with a payment method
  And I visit a buy now page
  And I have entered my country "USA"
  And I click calculate shipping cost
  When I click buy
  Then I can see the total cost "150.0"

```
