# Running real work with AI agents: roles, gates, and where oversight failed

*Field notes from a small company that runs engineering, infrastructure and media production with AI coding agents. Written from the author's own answers; translated and edited with Claude.*

## What the agents do
I use agents for code development, debugging, testing, documentation and reviewing experiment results in my own product and infrastructure work. In video production, scriptwriting, voice trials, quality control and editing are split into separate roles. On the HPC side we are working on agents that guide users and prepare their working environments.

## How the roles are split
I set the goal and the operating boundaries. A planning role breaks the work down, an executor prepares the change, and a verifier reviews tests and outputs. For consequential results I do not rely on the executor's summary: I ask for logs, files, measurements or evidence from an actual run. The final decision and the responsibility stay with me.

## What they cannot do without my approval
Changing the configuration of live infrastructure, widening access permissions, deleting data, terminating user jobs and making financial commitments all require explicit approval. Inside boundaries I have set in advance, agents can run inspections and small tests without asking at every step. A permission classifier in the coding tool adds a second, independent gate: it has blocked agents from merging unreviewed pull requests, deploying to production and writing to shared production data, even when an agent had been told to go ahead.

## Real cases
- **A check that existed but did not work.** In a video job, the quality agent gave a "conditional pass" to clips even though its own speech-to-text transcripts showed the mispronunciations. Having a verification step did not make the verification effective. We turned the observation into a hard rule: a wrong key word in the transcript is a fail, with no conditional pass.
- **Caught before users saw it.** In an HPC pilot, some files arrived with the wrong user ownership. We caught and fixed this before opening the environment to the user.
- **A passing test that proved less than it seemed.** In another test, GPU visibility inside the environment was verified, but the actual Gazebo application failed in the same environment. The first test should not be read as "the whole application works".

## Main lesson
Adding a separate verifier agent is not enough on its own. The verifier needs access to the right evidence, explicit acceptance criteria, and the authority to stop progress when needed. For me, reliability means repeatable tests and bounded permissions, not a convincing report.
