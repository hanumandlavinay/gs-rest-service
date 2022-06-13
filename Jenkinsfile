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
           
           // sh 'aws ecr --region us-east-2 | docker login -u AWS -p eyJwYXlsb2FkIjoid0lCQUJ6bGhWWWl1SzFsQ3ZIUnVzdGFoY2JqcjM5MVFQNS92TFY5MWl2MURlM0lHYmVTMjFqdlF4Q1ZnNGd6WXpiMEUzVURlS2VaNExCbVVxR3lHVGRZRnRPNWlXZ3lBcHgxZTVWVFRMZnozdVJpOXlyQnN6QWVuOEhubU45MXA0cHNrTlIxRlVtZXRPQWhtaEtSaVF3VVRlWUxoUFF5eDJGYWdxVnZVckRLbCtZUm5ESU1iemxpakJxWE00aS80SjRwY3Y3N2I4RnR4aWd1QzlFdHY3WFE1RThQZjZDaE9NN2xZblRkcmU0TVh1RVVNVXJPMVhQckVuSlAzUGJNaTViTzFkSDhJN3N3czhsbHFEc3JWQXNkd1BFMWVOeWhvUW1ETE00NksvQlVnV2FBVHBZV3FLa3ZGVzZIL3VsOU11TXpEZWNwV2hjeFNKTTdLVzU4U2JxTUY0T1RZY0VqbWR1VWlydC9ReVNUM2gyMGhLQ215WHo4bnBoYk9qVURhbGE4SENUeXVxbTJ0dXdMeWhJTnZ2cTZkU08vQXhxdWpWM21SQTQxTm9qOG5teW5zcmJoSnhFcjMrMHNzMlA2QTdRYVJYRnZLbHN1Q2orbTN3VmZyeE9QWGJvam9STnlSWjFtaHhmcnpzcXp6QVdMcmxyaDFTWjg0YnFQV0NWOWtLZi9xNFBvTVluWnFRQ3ZiRjRiWk40QnNrdUx2SHdPUWZodXhqMmk4UjBzekoxQlRZa1F4N3hSNERZNmQzdjVZRzhvZ3lhcTdRSWxwQXdtdHFmNjU5UWRiYWJGTDJ5eWsrLzhpWnhleGdSdmxIRmNENXFTdnJzUG04VVNjN1lWUnBydCsrL3VlZnNNSit1bHFUeWZodU40VjIxSG56UzZHWDY5UnlGTVYzWU9wc1ZNcHRBbFpodjZNbEJ6NFE0L3JXMGxHVTBWMHRNVlg1QjhnNEg0ZVdRaXNqNUhTNnIzU2lERkQ5K3FHUGkrTzc3Rll4NFNXNXRrT0swQ3pYM3FTL2JSSE9wcWpGTGR0OE1GU3g2czQ4M1MzaVhHMGt6RldRTUhQblZHRnZoeUJ2TW9GNENhOGZLODJRdWxPaXJlcjFldzR5Smpkcjl2TlAxYU42NEkwSmpyaEovZ0dIN3dselAwNFdRY1JqVzVRWWRyd3VJMjZBSVBaT3luVFJ2dzVzZkZvcVFHdUtZclRWSUcrbjFjb1JOR0VHcjczZlg3TlJLWDZjajBEVlM4ZDBmcm5lNEk4ZHQ5d0o3M3NPQXVmL0d4US9ESjRmNlBraHRWa2h3b2pxQmZidytjZUtlMEc1OWdSVDhBRVRMdDR3QXZMa1QwLzg4OE5qaTBuVVdPMDlselNINUlGWm14NUFHS01MUT09IiwiZGF0YWtleSI6IkFRRUJBSGpCNy9pZ3dNZzROUHdhdXJ4U0lZeDRIZm54dUdjLzQ4YkR3dndEcE5ZV1pnQUFBSDR3ZkFZSktvWklodmNOQVFjR29HOHdiUUlCQURCb0Jna3Foa2lHOXcwQkJ3RXdIZ1lKWUlaSUFXVURCQUV1TUJFRURKNCtDRjdnZTQxbnJkaWYyd0lCRUlBNzlyZTVpdGhsZ0FZYzFOK1dhbFhNbHVPQmZCOXI0bS9BQ0RLTTNUeHZ2d2VFRW5tSFVZTzdEWXhZbmVMcS9ieVdsTDFYUjNJQVZLVDhhSlE9IiwidmVyc2lvbiI6IjIiLCJ0eXBlIjoiREFUQV9LRVkiLCJleHBpcmF0aW9uIjoxNjU1MTU5Mjk5fQ== 817421948276.dkr.ecr.us-east-2.amazonaws.com/gs-rest-service'
           // sh 'aws ecr --region us-east-2 | docker login -u AWS -p  $(aws ecr get-login-password --region us-east-2) 817421948276.dkr.ecr.us-east-2.amazonaws.com/gs-rest-service'
           sh 'aws ecr get-login-password --region us-east-2 | docker login --username AWS --password-stdin 817421948276.dkr.ecr.us-east-2.amazonaws.com'
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
