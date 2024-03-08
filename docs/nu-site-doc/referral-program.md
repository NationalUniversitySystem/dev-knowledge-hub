# Referral Program

The student referral program allows an existing NU student to refer prospective new students to NU. The student who creates the referral gets a $50 gift card for each referral, and the referred student gets a tuition discount.

There are 2 pages, and 2 separate forms associated with the referral program:
- [www.nu.edu/refer-a-friend](www.nu.edu/refer-a-friend) -> Creates the referral (uses form ID 107 - "Refer a Friend")
- [www.nu.edu/refer-a-friend/redeem/](www.nu.edu/refer-a-friend/redeem/) -> Redeems the referral (uses form ID 101 "RFI - Refer a Friend")

We also use 2 API's that are not owned by us:
- We use an external third-party platform called [Ambassador](https://www.getambassador.com) to manage, track, and reward student referrals.
- We use an internal IT-owned API endpoint to lookup a NU student ID for a valid @student.nu.edu email address.

## Process flow:
1) Existing student enters their info into the referral creation form.
	- The submission email address MUST be a valid `@student.nu.edu` otherwise initial form validation will fail
2) Upon valid email address, the form sends an API request to an endpoint owned by the NU IT team. This endpoint takes the `@student.nu.edu` email address and returns the **NU Student ID Number** associated with it.
	- If the API returns null or undefined, user presented with a "we are unable to find your information" message.
3) Upon a valid student ID being returned, an API request is sent to an endpoint on the external Ambassador referral platform.
	- This creates the student as an "NU Ambassador" in their platform, to track future referral activity.
	- Upon success, the API returns a unique shortlink URL
4) The student can then copy their unique shortlink and send to friends/family, post to social media, etc.
5) When a prospective student clicks on the shortlink, it takes them to nu.edu/refer-a-friend/redeem, and auto-populates a hidden field to set it to the referring student's NU ID number.
	- When this RFI is submitted, this form submits as a normal RFI to sparkroom
	- It also submits a webhook to Ambassador so the referring student receives credit.


## Enrollment Advisor Feature
- On the referral creation page, the form is capable of reading a **?enradv** URL paramater. i.e `www.nu.edu/refer-a-friend/?enradv=8675309`
- This parameter is OPTIONAL. If it is provided, it will attach a hidden "enrollment advisor" field value to the form when it is submitted.
- This enrollment advisor will be attached to the student's Ambassador platform account, thus allowing enrollment advisors to receive credit for referrals as well.

## A note on testing
- Important note that the referral creation form requires a **valid** @student.nu.edu email address.
	- If the email provided doesn't match a `@student.nu.edu` regex, front-end form validation will fail.
	- If the email provided does match the regex pattern, but is not actually an enrolled NU student, IT's API will return null.
	- This means we have to use real student emails to test. We can't just use something like `testing@student.nu.edu`.
- Ambassador platform seems to have some sort of dedupe validation logic - if you re-use the same student email to signup multiple times within a certain timeframe (i.e. when testing), only one will show up. This makes sense from a process perspective, but makes it difficult to accurately test.


## Student Lookup API

Custom API endpoint owned by IT

Endpoint:
`https://student-ambassador-verification.azurewebsites.net:443/api/verify-student/triggers/manual/invoke?api-version=2022-05-01&sp=%2Ftriggers%2Fmanual%2Frun&sv=1.0&sig=Ww5WUcvWbOuCOuYfM47My2x7eBMwgXOhwEd7JPXKCyk`

Accepts a **POST** request

Body JSON needs to consist of a valid student email address:
```json
{
    "email": "m.khrangtong3084@student.nu.edu"
}
```

Should return JSON response containing the Student ID associated with that email address:
```json
{
    "StudentId": "041603084"
}
```

### Prior Versions
A prior implementation of this referral program used a referral creation form that was a full embed from Ambassador -- embedded javascript code snippet triggered a popup that contained the Ambassador-hosted form. This worked as an initial proof of concept, however it left no room for additional business logic. So now we run it through GravityForms and custom APIs.
