# Code Location

**TODO**: Define how to capture the location of the code. Should support Git (repo, file name(s), code lines), non-Git (e.g., a statement that it was from a local file optionally with the ability to capture the code), etc.



Some rough examples (delete after finishing)

```yaml
# some examples of ^^  
      # Non-Runnable - [pointer to part of an existing code base, not indepenandtly runnable]
      # Runnable - [independanrtly runnable: docker image; python func OR script w/ conda/requirements.txt]
    runnable_docker: #indicative, to be specified by eng
      - env:
        - key: [string]
          value: [string]
        entryPoint: [string]
        resources: [tbd]
    runnable_python: #indicative, to be specified by eng
      - sourceCodeRepo: [Git URI]
      - fileNames:
        - name: [string]
        - lines: [array of int]
      - pythonVersion: [enum]
      - requirements: [tbd to capture requirements.txt conda.yaml]
    nonrunnable_git: #indicative, to be specified by eng
      - sourceCodeRepo: [Git URI]
      - fileNames:
        - name: [string]
        - lines: [array of int]
```
