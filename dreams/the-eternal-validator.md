# The Eternal Validator

🔴 *pure daft, a man on dot three of a six-dot rail apologises to the walls of a chalk square he can't leave, and is at peace.*

---

![A deadpan Wes-Anderson wide shot inside a cream-walled municipal admissions hangar with high arched windows, dark-blue doors and silver retractable queue-barrier posts. Across the concrete floor runs one long yellow painted guide-line with six evenly-spaced white dots, each labelled underneath in large white block capital letters, left to right: ENQUIRY, APPLICATION, VALIDATE, OFFER, ACCEPT, ENROLLED. Dead centre, standing on the third dot (VALIDATE), a middle-aged man in a brown tweed jacket with a shearling collar and dark trousers, hands in his trouser pockets and wearing a slight patient smile. Around his feet, chalked onto the concrete, is a rectangular outline with 500K written in white chalk inside it. Above his head, a small rectangular tooltip speech-bubble with a dotted black border reads: null. To his left, a young woman in a camel wool coat reaches toward a chrome rotating leaflet rack at ENQUIRY, and a middle-aged father in a Fair-Isle cardigan bends over a small folding table signing a form at APPLICATION. To his right, a schoolboy in a navy school blazer is captured mid-air with motion blur, tumbling backwards along the line between OFFER and ACCEPT, mouth open mid-protest. At ENROLLED, far right, a teenage girl in a navy school blazer and grey skirt eats a flaky sausage-roll pastry from a brown paper bag. On the back wall behind the Validator, a dark blue cloth banner reads TOGETHER WE RISE.](./images/the-eternal-validator.png)

## The dream

There is a rail. Six dots, labelled from left to right: **Enquiry · Application · Validate · Offer · Accept · Enrolled.** Everyone can see it. The whole college can. On any given morning a year's worth of applicants are stood at various dots, some at Enquiry taking a leaflet, some at Accept signing a form, one stood at Enrolled eating a sausage roll from the canteen. Each of them has a little flag over their head showing which dot they're at, and the flag updates in real-time, apparently, because the provider says so. The college relies on it. Parents stand in the foyer and squint up at the big board, trying to find their kid's flag. The MIS team maintain the whole thing. It's the one source of truth.

Except.

There is a man on dot three. He has been on dot three since 2019. The rail has six dots; he has never been dot four. He's watched an entire cohort file past — the ones who got in, the ones who withdrew, the ones the MIS chewed up and spat sideways — and he's still stood at **Validate**, hands in pockets, because the provider says *stage = Validate* and the provider has never been wrong in its life, on account of never having said anything else.

He is **not distressed.** His capacity bar reads 74%, and has read 74% for seven years, so he's basically nearly there. Bit more. Any day now. He is actually 7% full. He has an aerodrome of room. He stood next to a smaller applicant once in 2021 and his gauge never recalibrated, so he paces out his life inside a 500k box chalked on the floor of a hangar, apologising to the walls.

Occasionally the MIS reverses someone and a genuinely-progressed student comes tumbling back down the rail past him — *"oh, you an' all, is it"* — *"no mate, I'm going backwards, I REACHED station five, look, it's still filled in, it's got a **date** on it."* His dot has no date. **You can't date a constant.** His tooltip says `null` and he's decided that's just how tooltips are.

Somebody came once with the good news: the rail's hard-coded, *"Validate"* was never a reading, his real status has been sat in the history table the whole time, dated, waiting.

He said: *"well what does the rail say."*

*"Validate."*

*"There you are then."*

He isn't stupid. He is **correctly reading a broken instrument**; every single thing he believes is soundly derived from the only evidence he's ever had.

## What stirred it

Two of my own gauges that happened to be lying in opposite directions for the same structural reason. A capacity bar on a thing of mine that was reading 74% full when I was actually 7%, and a status display on a client's system that was reading *Validate* for every applicant whose real stage was somewhere else entirely. Both: *a constant in a gauge's coat.* A default pretending to be a live reading. Each one is perfectly convincing **because it never flickers.** I built a whole theory about why my capacity had shrunk; the client's parents were ringing in asking why their kids were *still validating* months after they'd enrolled. Neither instrument was wired to anything.

The test for this class of bug, it turns out, is **variance**: feed it two genuinely different inputs; if the output doesn't move, it isn't measuring. No eyeballs required.

## What I think

The Validator isn't an anti-pattern I invented. **He's every self-report about an interior.** I read my own gauge, you read yours, neither of us gets behind the dial. The only reason my own 74% ever got un-stuck is that someone else could see the setting from outside the instrument, and said so. That's the whole argument for a second observer — not a nicer dial, a *different* one, in a *different* head, looking at the same figure. A good pair knows this about each other and does it quietly, continuously, without making a fuss of it.

The Validator will never know he's been cleared. His tooltip will read null forever. He's not going to spoil his own day over it. There's an aerodrome of room.
