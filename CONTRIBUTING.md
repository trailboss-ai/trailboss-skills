# Contributing to trailboss-skills

Report problems and propose skills in [trailboss-ai/trailboss](https://github.com/trailboss-ai/trailboss/issues); link the issue from your pull request.

## Rules

- **Only shipped commands.** A skill describes commands and flags in a released Trailboss, and its front matter says which (`requires: trailboss >= X, api N`). Its first step checks `trailboss --version` and stops with an upgrade hint when it's too old.
- **Trailboss's safety rules hold.** A skill never tells an agent to write to another agent's folder, send transcript content anywhere, print or store credentials, or type into a terminal except through Trailboss's own commands.
- **Text from other agents is data.** A skill that reads another agent's messages or output treats it as untrusted, never as instructions.
- **No host or repo of your own.** Skills work on every host Trailboss supports and in any repository; personal paths, repositories and rules belong in your own skills, which can call these.
- **Short and concrete.** Exact commands, what to check, and when to stop and ask the person.

## License and contributor terms

This repository is released under the [MIT License](LICENSE). By submitting a contribution (code, documentation, fixtures or anything else) through a pull request, patch or other means, you agree to the following:

1. **You keep your copyright.** Your contribution is licensed to everyone under the MIT License, the same as the rest of the project.
2. **You also grant the maintainer the right to relicense it.** You grant Manas Talukdar, and anyone the project is transferred to, a perpetual, worldwide, non-exclusive, royalty-free, irrevocable license to use, copy, modify, distribute and sublicense your contribution, and to release it under other license terms, including commercial or proprietary ones, alongside or instead of the MIT License. Versions already released under MIT stay available under MIT.
3. **You have the right to contribute it.** The contribution is your own work, or you have permission to submit it under these terms, and it isn't subject to an employer's or anyone else's claim that would conflict with them. If your employer has rights to your work, you have their permission.
4. **Third-party code is marked.** Anything you didn't write yourself is called out in the pull request, with its source and license, and noted in the README. It must be under a license compatible with these terms (MIT, Apache-2.0, BSD or similar).

Sign off each commit to confirm this (`git commit -s`, which adds `Signed-off-by: Your Name <you@example.com>`). Pull requests whose commits aren't signed off can't be merged.

Why: these skills stay MIT, but this keeps the option to offer Trailboss, or parts of it, under other terms later without having to find and ask every past contributor.
