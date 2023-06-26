# Commit Message Format

🚀 此規範參考自[AngularJS Git Commit Message Conventions
](https://docs.google.com/document/d/1QrDFcIiPjSLDn3EL15IJygNPiHORgU1_OOAqWjiDU5Y/edit#heading=h.uyo6cb12dt6w)

每個`commit`由標題(header)、正文(body)和頁腳(footer)組成。

```
<header>
  <BLANK LINE>
    <body>
      <BLANK LINE> <footer></footer></BLANK></body
  ></BLANK>
</header>
```

## Commit Message Header

使用祈使句、現在進行式：使用「change」而不是「changed」或「changes」
頭文字不需要大寫
尾巴不要加句號 (.)

```
<type>: <short summary>
  │            │
  │            └─⫸ Summary in present tense. Not capitalized. No period at the end.
  │
  │
  │
  │
  │
  │
  │
  └─⫸ Commit Type: build|ci|docs|feat|fix|perf|refactor|test|chore
```

### Type

Must be one of the following:

- build: Changes that affect the build system or external dependencies (example scopes: \* gulp, broccoli, npm)
- ci: Changes to our CI configuration files and scripts (examples: CircleCi, SauceLabs)
- docs: Documentation only changes
- feat: A new feature
- fix: A bug fix
- perf: A code change that improves performance
- refactor: A code change that neither fixes a bug nor adds a feature
- test: Adding missing tests or correcting existing tests
- chore: Clean up code or something does not bellow above

## Commit Message Body
使用祈使句  
詳細描述這個`commit`的變更原因


## Commit Message Footer(optional)
The footer can contain information about breaking changes and deprecations and is also the place to reference GitHub issues, Jira tickets, and other PRs that this commit closes or is related to. For example:
```
BREAKING CHANGE: <breaking change summary>
<BLANK LINE>
<breaking change description + migration instructions>
<BLANK LINE>
<BLANK LINE>
Fixes #<issue number>
```
or
```
DEPRECATED: <what is deprecated>
<BLANK LINE>
<deprecation description + recommended update path>
<BLANK LINE>
<BLANK LINE>
Closes #<pr number>
```
Breaking Change section should start with the phrase "BREAKING CHANGE: " followed by a summary of the breaking change, a blank line, and a detailed description of the breaking change that also includes migration instructions.

Similarly, a Deprecation section should start with "DEPRECATED: " followed by a short description of what is deprecated, a blank line, and a detailed description of the deprecation that also mentions the recommended update path.

## Revert commits
If the commit reverts a previous commit, it should begin with `revert:` , followed by the header of the reverted commit.

The content of the commit message body should contain:

information about the SHA of the commit being reverted in the following format: `This reverts commit <SHA>`,
a clear description of the reason for reverting the commit message.