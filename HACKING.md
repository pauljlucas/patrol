#### Hacking the Patrol stack

Because `patrol` includes both the rulesets and `lambda-cfn` in its `package.json`, developing new functionality could require several roundtrips through Github. 

Instead, leverage `npm link` to link in the development dependency. For example, if working on `lambda-cfn`, the workflow would look something like:
- Once finished with modifications to `lambda-cfn` link it to `patrol`

	```bash
	cd lambda-cfn  #modified version
	npm link
	cd ../patrol
	npm link lambda-cfn #links in the modified version
	npm install #installs the remaining dependencies but skips lambda-cfn
  export LAMBDA_TASK_ROOT=$PWD #insures /patrol is used as the app root
	```

- To remove the development version (nodejs v0.10.x)

	```bash
	npm r lambda-cfn -g
	```
