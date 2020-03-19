# Solargraph Practices
My collection of Solargraph best practices and setup

## Useful links

Solargraph site - https://solargraph.org/
Solargraph github repo - https://github.com/castwide/solargraph
Solargraph extensions for different editors - https://github.com/castwide/solargraph#using-solargraph

## Solargrap setup

### Visual Studio Code

1. Install solargraph gem `gem install solargraph`
2. Install https://github.com/castwide/vscode-solargraph extension
3. Add this to your personal config
```json
"solargraph.formatting": true, // enable formating through rubocop
"solargraph.transport": "external", // enable usage of external solargraph server. see below for details
"solargraph.externalServer": { // external server settings. there're default ones
  "host": "localhost",
  "port": 7658
},
```
4. Start solargraph server and restart VS Code
5. You're done

### Sublime Text 3

1. Install solargraph gem `gem install solargraph`
2. Install LSP package: Ctrl+Shift+P -> Package Install -> LSP
3. Modify LSP package settings
Example of my setup [here](https://gist.github.com/denis-mokreckiy-itechart/e170c1c5f9d74561ad4b01f055ee9182)
4. Start solargraph server and restart Sublime Text 3
5. Enable LSP for ruby: Ctrl+Shift+P -> Enable Language Server Globally or in Project.
6. You're done.

### Solargraph server setup

1. Install solargraph gem `gem install solargraph`
2. Run code scan `solargraph scan -v`. It will show if index process is successful or not (exceptions or errors).
3. Run yard documentation generation for project `yard doc`
4. Run yard documentation generation for gems (optional) `yard gems`
5. Run yard documentation generation for rails `solargraph bundle`
6. Add this [file](https://gist.github.com/castwide/28b349566a223dfb439a337aea29713e) to your project root 
7. Run documentation for you current Ruby version `solargraph download-core 2.6.5`
Available documentation is available through `solargraph available-cores`
8. Run solargraph server with yard (yard is optional)
I use separate tab/procman/overmind/docker not to depend on project settings
`Procfile.dev`
```
solargraph: solargraph scan && RUBYOPT=--jit solargraph socket
yard: yard doc && yard server --reload
```
where
```
solargraph scan && RUBYOPT=--jit solargraph socket
```
Scans project (around 20-30 secs) and starts Solargraph server with Ruby JIT (helps in a long run). You can add `RBENV_VERSION` (rbenv ruby version to use) or RVM analog to run server with desired Ruby version
```
yard: yard doc && yard server --reload
```
Scans project for documentation changes and starts yard server

## Support

I will try to keep this README up-to-date. Feel free to open issues or PRs.
Any feedback or support is welcome.
