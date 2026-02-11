When verified author is publishing new book:
- Admins receive new message of the book 
- They moderate it:
	- Reject 
	- Approve 
- On both endings authors receive a message.

**Flow**:
1. User submits a *book* (image, description, title, price)
2. Book image is uploaded and *publicId* is passed to next step.
3. New *ModerationRequest* is created on the server:
	it references the author and has all the book data including the publicId of the image
4. Admins on the admin page see new message on the *dashboard* which is fetched with *useEffect*. 
5. Admin can reject or approve the book.
	- If <mark style="background: #FF5582A6;">rejected</mark> -> the image is deleted from the cloud and the status of the ModerationRequest is set to rejected
	- if <mark style="background: #BBFABBA6;">approved</mark> -> new book is created