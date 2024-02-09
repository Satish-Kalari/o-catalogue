#!groovy
@Library('o-robo-shared-library') _

// responsibility to pass what type of application and componenet is this to pipleline desission 

def configMap =[
    application: "nodejsVM",
    componenet: "catalogue"
]
if( ! env.BRANCH_NAME.equalsIgnoreCase( 'master' ))
pipelineDecission.decidePipeline(configMap)

else{
    echo "This is PRODUCTION, deal with CR process"
}