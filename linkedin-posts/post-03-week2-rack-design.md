# LinkedIn Post 03 — Week 2 Rack Design
**Date:** 2026-03-15
**Status:** Ready to publish

---

🔧 **Week 2 in the homelab. Nobody told me rack design was 80% philosophy and 20% cable.**

Last week I broke a router with a debug command. This week I spent three hours debating where to put a patch panel.

Progress.

Here's what Week 2 actually taught me:

---

📐 **Lesson 1: 0.25m cables are optimistic**
I ordered a beautiful colour-coded set of short patch cables. Magenta for data. Blue for OOB. Red for vMotion. Very professional. Very enterprise.

Then I measured the actual distance between my switches and the patch panel.

I am now also ordering 0.5m cables.

---

🗂️ **Lesson 2: Plan the rack on paper before touching the rack**
I moved my patch panel three times. On paper. Which is exactly the right place to move it.
Front cabling, rear cabling, airflow gaps, shelf depths, port face directions — every decision affects the next one. A 42U rack is not just a metal cupboard. It's a three-dimensional cable routing problem with power constraints and an airflow agenda.

---

🔌 **Lesson 3: Shelves eat U space faster than you expect**
19" shelves: 2U each. I have five of them.
That's 10U of rack space dedicated entirely to holding things that would prefer to be rack-mounted. File under: things that seem obvious in retrospect.

---

↕️ **Lesson 4: Left and right are always from the front**
This sounds trivial. It is not trivial at 11pm when you're standing behind a rack trying to remember which side the PDU is on.
Standard convention: left/right is always referenced from the front of the rack. Document it. Save future-you an argument with past-you.

---

🏆 **The meta-lesson:**
Good infrastructure isn't built — it's designed, revised, questioned, and then built. Every layout decision we made this week has a documented reason in the repo. When something breaks in six months, I'll know exactly why we made that choice and whether it was right.

The rack isn't cabled yet. But the plan is solid, the orders are placed, and the colour-coding spreadsheet is disturbingly satisfying.

~35% through the build. Servers still need rails. The 3850 is on its way. The grind continues. ☕

📁 Full build log: https://lnkd.in/eA5-2vVb
🐙 GitHub: https://github.com/TheITchef

#homelab #cisco #networking #rackdesign #infrastructure #itpro #hybridcloud #linux #microsoft #cablemanagement
