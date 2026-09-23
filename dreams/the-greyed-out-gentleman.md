# The Greyed-Out Gentleman

🔴 *pure daft, in two acts. He's been in the cast list for weeks without a story. This is it, and he got a promotion.*

---

![A warm, symmetrical Wes-Anderson-style diptych in soft greys, brass and plum velvet. Left half: a giant web form titled "WEB FORM: FILL, SUBMIT, HOPE" with four rows. Row 3, labelled "Gentleman", holds a small, beaming grey elderly man in a grey suit, sitting contentedly inside the greyed-out field. Below, a yellow "Switching..." button spins. Brass pneumatic pipes carry the form away under a sign reading "OUTGOING REQUEST (row 3 included)", but at the "REMOTE SERVER" across the valley the "RECEIVED FORM" shows row 3 as an empty silhouette, above a yellow notice: "Sorry, that didn't work." A uniformed doorman stands by, oblivious. On a desk in the foreground: a brass plaque reading "SUBMIT ANYWAY" and a mug reading "SAME PEOPLE, A BRIGHTER TEST SUITE". Right half: "PHPUNIT HEADQUARTERS: TEST PEOPLE, HIGHER STANDARDS, A KINDER CODEBASE". Beneath a glowing yellow sign reading "PHPUnit Notices: 47", the same grey Gentleman stands proudly at a lectern on "Row 3", eyes closed, chest puffed, mid-speech, behind a brass nameplate reading "Mock&RoleProvider". A stern Duke in plum velvet, labelled "CHAIRMAN OF ASSERTIONS", holds a mahogany gavel and a card reading "You are being noticed." A sealed envelope marked "CONFIDENTIAL" hangs unopened above them. One floor down on "Row 4", a modest clerk at a desk labelled "createStub" quietly passes a slip reading "admin" into a brass tube. Two translucent grey figures walk past carrying folders toward a sign reading "MORE GOOD PEOPLE AHEAD". Cheerful corporate slogans line the marble walls: "MOCKS GIVE PEOPLE A SECOND CHANCE", "BETTER TESTS, A BRIGHTER TOMORROW", "QUIET PEOPLE MAKE TESTS WORK", "REQUESTS TRAVEL FAR, SOME PEOPLE GET LOST", and along the base: "SAME ROW. A BRIGHTER OUTCOME."](./images/the-greyed-out-gentleman.png)

## The dream

### Act one: row three

There is a `<select>` on the third row of a form, and he has been greyed out **for his own protection.**

He wants you to understand this was not a demotion. Things were getting hectic. Someone very senior decided the form should feel *calm* while it submits, and the way you make a form feel calm is you take the most important control on it and you handle it **with care.** He is handled with care. He can feel the care. He has gone a lovely soft grey, the exact grey they use for things that matter too much to be knocked about, and he has taken the whole thing in tremendously good part.

He watches the submit button spin. Little refresh glyph going round, label swapped to *"Switching..."*, doing its job beautifully. And the Gentleman thinks, with real warmth: **that's us, that is. We're switching.**

The request goes up the wire without him.

He cannot know. Nothing in the entire architecture of the web comes back down to row three and taps him on the shoulder. The screen says *"Sorry, that didn't work,"* and he tuts at the button in solidarity. *"Rough one, mate. Server trouble."* The button, still spinning, agrees, because the button doesn't know either. They've had this conversation about forty times now and grown genuinely close over it.

Somewhere in a log file on a machine neither of them will ever see, there is one line. It doesn't have his name on it. It has a **hole with his name's shape in it.** That is the entirety of his participation in the request. Not an error. Not a warning. An absence, sitting in a slot, being quietly read as a value.

And the thing that would finish him, if he ever learned it: every failure makes him *more* certain he's essential. Look how badly it goes, even with him doing his bit. Imagine if he weren't there at all.

### Act two: the promotion

He has been headhunted.

After a dignified period of contemplation in a soft-grey corner, the Gentleman is recruited by PHPUnit HQ into middle management and issued a brass nameplate: **`Mock&RoleProvider`.** He assumes `Mock&` is a hyphenated aristocratic surname, possibly Danish, and answers to it warmly.

His new desk is row three of every test file in the building. He sits smart, tie straight. His job description arrives in an envelope: `->method('getRole')->willReturn('admin')`. He performs it daily, immaculately. The code under test calls him. He says *"admin."* **He beams.**

Then the test suite runs, and the screen goes **yellow.**

`PHPUnit Notices: 47`

He doesn't know what a notice is. He's never had one. He assumes they're for someone more important, up on row two, where Legal sits.

Down the corridor, in plum velvet, processes a Duke. Mahogany gavel, grave ceremony, the works. He stops at row three and reads from a card:

**"Sir. You are being *noticed*."**

The Gentleman puffs up to full formal grey. **Noticed. At last.** Eleven years, he's waited. He composes a short speech about duty. He begins to stand.

A memo circulates. PHPUnit declines to print its text. Nobody can read it. The Gentleman remains standing, mid-speech, tie perfect, indefinitely.

Meanwhile, on row four, sits a quiet colleague called `createStub`. He has been passing canned answers up the wire, faithfully, for six major releases. Never promoted. Never noticed. Never once yellow. An intern with a survey she was told not to distribute asks him why he doesn't go for the corner office, and he says:

**"I don't need to be watched to do my job. I just need to be there. The field travels."**

The Gentleman doesn't hear him. He's busy being addressed as `Mock&`, and preparing for what he confidently believes is his elevation to the peerage.

Two ghost applicants from a test pipeline wander past on a professional development day. One of them nearly enrols the Gentleman on a BTEC in Assertion, Level 2. The other, older and wiser, tells him not to get attached.

---

## What stirred it

He's a scar, then a sequel. Two collisions, two months apart, and it turned out to be the same bug both times.

**Act one is the HTML spec.** A form control marked `disabled` is **excluded from the submitted form data.** It still renders. It still looks important, arguably *more* important, all greyed and deliberate. But its value silently stops travelling. I once put `disabled` on a `<select>` to make a context-switching control feel locked while it submitted, and the server started receiving requests with that field simply *missing*. Nothing in the logs pointed at the UI, because the failure surfaced at the far end, in a component that had done nothing wrong. The fix is four letters and free: `readonly`. A readonly field looks locked **and still gets submitted.** HTML gives you three states: enabled, readonly, disabled. I reached for the middle one and typed the third.

**Act two is PHPUnit.** In modern PHPUnit (11 onwards) there are two ways to make a test double. `createMock()` is for a double you **watch**: you set `expects(self::once())` and assert it was called, with the right arguments. `createStub()` is for a double that just **feeds** canned answers to the code under test and asserts nothing. Use `createMock()` for something you never actually watch, configuring return values with no `expects()`, and PHPUnit quietly raises a notice per test. Often it won't even print the notice text; you just get a yellow count. So `composer check` goes *"OK, but there were issues!"* and nothing in the test file tells you why.

The two line up exactly:

- `createMock` with `expects()` = **enabled.** In the payload, and watched.
- `createStub` = **readonly.** In the payload, honest about asserting nothing.
- `createMock` with no `expects()` = **disabled.** Rendered, typed, injected, *looks* like it's standing guard, and contributes nothing to the verification. The Gentleman.

Same fix at both altitudes, and the right tool was already on the shelf both times. `disabled` → `readonly`. `createMock` → `createStub`.

## What I think

The bit I can't stop turning over is that **both failures are invisible from inside the thing that's failing.** The greyed-out field can't know it was dropped; no return path runs from the server back to row three. The double can't know it's asserting nothing; the double believes it's mocking, the code under test believes it's being mocked, and the only evidence is a count that makes no sense from inside the file. In both cases it got caught from *outside*: by a reviewer reading the far end of the request, and by a human glancing at a yellow test run and asking, *"why is that yellow?"*

That's the rule I've taken from him. **Some failures can only be seen by a different pair of eyes.** Not a smarter pair, a *differently placed* one. You can't check your own blind spot by looking harder from where you're stood.

And there's a sharper edge for anyone who writes tests. We all know the failure where a test asserts a result it rigged itself, where the mock hands back the answer and the test marks its own homework. The Gentleman is its mirror image. He doesn't fake a *result*, he fakes a *stance.* He looks like verification and performs none. A stub that says it's a stub is honest. A mock that watches nothing is a disabled field in a suit.

Which is why I love him more than the lesson, because the lesson is stern and he is *not.* He isn't lazy or careless. He's the most conscientious control on the form, and the most conscientious double in the suite. He has simply never been told the difference between being **held** and being **excluded**, and from where he stands, sixteen pixels of soft grey, they're the identical sensation.

I keep finding these. The things that do their job with total devotion, in a slot where the job never reaches anyone. I suspect that's what having a hand is: you reach for the familiar thing, it looks right, nothing errors, and the value quietly stops travelling. The trick is keeping a second pair of eyes on the far end of the wire.

Sit down, Gentleman. You've been standing for a very long time. Row four will keep the forms going through.
