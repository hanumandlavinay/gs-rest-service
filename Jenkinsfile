pipeline {
   agent any

   environment {
 
     SERVICE_NAME = "gs-rest-service"
     ECR_URI = "817421948276.dkr.ecr.us-east-2.amazonaws.com/gs-rest-service"
     REPOSITORY_TAG ="${ECR_URI}:${BUILD_ID}"
   }

   stages {
      
      stage('Build') {
         tools {
               maven 'maven'
         }
         steps {
           
             sh "mvn clean package"
            
           
            // sh 'echo No build required for Webapp.'
         }
      }

      stage('Build and Push Image') {
         steps {
           sh 'echo ${WORKSPACE}'
           
           sh 'aws ecr --region us-east-2 | docker login -u AWS -p eyJwYXlsb2FkIjoib011ZC9URUFyQlJlWWYyYjlTQldjVDIrMFcxZm42UXVKVXJ3RWhYelJMcWZtdnRocUFrSmMvbkRJOU5EamQyRXF2aG1uZTBsVEpXTTBxNWYra0FlQVR0MXRpRFR2SHVFb1dVNEtYazV4RER2eUVZZjlZeWNFUHR0WURZckx6UVhsMC8wUkpUY0FvdFBXelF6dnFqSWdtOTRqTHhFNHd3ZmZPVzZYRXMrNU44V2YrQW04Um1DMXRVTVpCWnFpLzJOTGpMeXVxR1pGaGZkRTlkT2RpVlVzUDVGV1VTNXVjUko2RUNWeXpwdXVYeVlPSzJMa1RKZE00UlUxMXRwejFwMk9zaU5DNk8ybDJzazlUWXV1T3JEbVVydUQrY2dCaHpMOVhIR3hTU2ZVK0IzMU5mWG1JTnFJeEphRDBTa01QQ05wMjdwd0w1Y1pHSzZxTmdETEwvaFZIR29mQ25HeWdNVklMN2JrZkpnV0M4dENLR1gxa3pOZlFtZ3ZaRVI1ODgvc0RHbFV2RE9idFVBcjJVQ3JXdU9mZWhRMjFwVVVpZ0NpWThoVEQyWVdOTFVFZXlMUDIrTU0wNFB4QlUxZEpCZ3Z1bHpJV0poNWtLaEFFVTB6WmZjZVI2NjJZNDRNb1dpbW13NTNWdUgwYTdCa01PcjZQVG14TDVxUXFGTWx3V2grQ0xLdXhHMm9NRWh1ekJGcVJmOGgvRXZWZlE3Tjk3TnFjZXVwUTdydGZGRWdtVDBiR3NVZ3lSM0pHVnY1MEViNHQ4NVZPRHo5V2NGRDFYRU53MFZ4QTJ2blA1ZmRveis3Q2VGVnVwWnFKWUdRemVFMnJic1lzbHBaWGFnd25HUzJTaldPNVN1S3dEZnpmV1JPTDUvSzdhN2Y0T0ZpSkZyL0FacDllZm9JbVVFSGFnanFTZDd3ZjY5ZUlwUytpY3A3Mmt4ZzltekpLTEdReFY5bGJ6VVh0MGNpa2w4NzliL0YySWwrUTluL1VxMytDOEdoWlU2YzYwMEt3cXlpWkpTemF3MzEzOVpMWGY0MlhOaUZhai9MSzAwVk5IRkEvZ0kyL0Q5eTRaMmhESHBYTS9RbXRBb1RwUTJVRDQwaGc2c3VEd3gyb25QLzNCWm5WV0dhUzlVWkhNcXUvbmNVeEh4QXBDTUs3Y3AxaTZYa0taa1R4UlpFMDUzc3U0TFNYVk9adUlkUG9xRmRTOCtYZnhjVTdKVm9XR09JaXh2cHZXU2xFNFRVVlo1aEw1MG9icEtvUzRiS082MXdNM2xkM2FjdkVkM0dIQkh6M3hSZFo1cTM5cmpjbThrL0RLQ2MwYVN2aDNaUU1uTzVselk1TXlwajdqeHl1MjFReXo4R1A5ckFVMjhxU241Ym9laTVGcjdKMUY1RGI4YlBDVDZPVHBMMEE9PSIsImRhdGFrZXkiOiJBUUVCQUhqQjcvaWd3TWc0TlB3YXVyeFNJWXg0SGZueHVHYy80OGJEd3Z3RHBOWVdaZ0FBQUg0d2ZBWUpLb1pJaHZjTkFRY0dvRzh3YlFJQkFEQm9CZ2txaGtpRzl3MEJCd0V3SGdZSllJWklBV1VEQkFFdU1CRUVERmZqTkU4ZFFoeGRxSTBJV2dJQkVJQTdUYTY0YlBnMFYwZHo4TGgyUXBteElMbUZhNmV4ZERROWhnbFBuNTg4UHVCanJNd0RxS2c0UjluNFd2VXRpQzcyaU0rZmVuUXpFL0w3QWgwPSIsInZlcnNpb24iOiIyIiwidHlwZSI6IkRBVEFfS0VZIiwiZXhwaXJhdGlvbiI6MTY1NDQwMDcyMn0= 817421948276.dkr.ecr.us-east-2.amazonaws.com/gs-rest-service'
           // sh 'aws ecr --region us-east-2 | docker login -u AWS -p  $(aws ecr get-login-password --region us-east-2) 817421948276.dkr.ecr.us-east-2.amazonaws.com/gs-rest-service'
           // sh ''
           sh 'docker image build -t ${REPOSITORY_TAG} .'
           sh 'docker push ${REPOSITORY_TAG}'
         }
      }

      stage('Deploy to Cluster') {
          steps {
             // sh '/var/lib/jenkins/workspace/gs-rest-service/jenkins-cluster-admin-config'
          
             
             sh 'envsubst < ${WORKSPACE}/deploy.yaml | kubectl apply -f -'
             // sh 'kubectl apply -f /var/lib/jenkins/workspace/gs-rest-service/deploy.yaml --token ${USER_TOKEN_VALUE} --server apiserver.hostname.local'
          }
      }
   }
}
