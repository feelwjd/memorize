
Github repo에 Jenkinsfile이 존재해야함
또는 FreeStyle로 직접 스크립트를 작성해서 수행 가능함.

# Jenkinsfile
- # Declarative Pipeline
	- 최상단에 pipeline 지시어로 시작함.
	- [문법 참조](https://www.jenkins.io/doc/book/pipeline/syntax/)


---

### 1. **Pipeline 기본 구조**


```groovy
pipeline {
    agent any            // Pipeline이 실행될 에이전트 정의
    stages {             // Pipeline에서 실행할 여러 단계 정의
        stage('Example') {
            steps {      // 각 단계에서 실행할 작업 정의
                echo 'Hello World'
            }
        }
    }
}
```

---

### 2. **`agent` 섹션**

Pipeline이 실행될 노드를 정의

- **`any`**: 모든 가용 노드에서 실행.
- **`none`**: 특정 stage에서만 노드 설정.
- **`label`**: 특정 라벨이 붙은 노드에서 실행.
- **`docker`**: Docker 컨테이너에서 실행.

```groovy
agent any            // 모든 가용 노드
agent none           // 모든 노드 비활성화, stage에서 개별 설정
agent { label 'linux' }  // 'linux' 라벨이 붙은 노드
agent { docker { image 'maven:3.6.0' } }  // Docker 컨테이너에서 실행
```

---

### 3. **`stages` 섹션**

Pipeline의 주요 실행 단계를 정의합니다. 각 단계는 독립적으로 실행

```groovy
stages {
    stage('Build') {
        steps {
            echo 'Building...'
        }
    }
    stage('Test') {
        steps {
            echo 'Testing...'
        }
    }
    stage('Deploy') {
        steps {
            echo 'Deploying...'
        }
    }
}

```

---

### 4. **`steps` 섹션**

각 stage에서 실행할 작업을 정의

```groovy
steps {
    echo 'Hello World'         // 콘솔 출력
    sh 'ls -la'                // 쉘 명령 실행
    script {                   // 스크립트 블록에서 Groovy 코드 실행
        def result = 'Success'
        echo result
    }
}
```

---

### 5. **`post` 섹션**

Pipeline 실행 후 실행할 작업을 정의

- **`always`**: 항상 실행.
- **`success`**: 성공 시 실행.
- **`failure`**: 실패 시 실행.
- **`unstable`**: 불안정 상태(예: 일부 테스트 실패)일 때 실행.
- **`aborted`**: 중단되었을 때 실행.

```groovy
post {
    always {
        echo 'This always runs'
    }
    success {
        echo 'This runs on success'
    }
    failure {
        echo 'This runs on failure'
    }
}
```

---

### 6. **`environment` 섹션**

환경 변수를 설정

```groovy
environment {
    JAVA_HOME = '/usr/lib/jvm/java-8-openjdk'
    PATH = "$JAVA_HOME/bin:$PATH"
}
```

---

### 7. **`parameters` 섹션**

사용자 입력 파라미터를 정의

```groovy
parameters {
    string(name: 'BRANCH', defaultValue: 'main', description: 'Branch to build')
    booleanParam(name: 'DEPLOY', defaultValue: true)
    choice(name: 'ENV', choices: ['dev', 'staging', 'prod'])
}

```

---

### 8. **`triggers` 섹션**

Pipeline을 자동으로 트리거

```groovy
triggers {
    cron('H 4 * * 1-5')           // 매주 월~금 4시 실행
    pollSCM('* * * * *')          // SCM 변경 확인
    githubPush()                  // GitHub Push 이벤트로 실행
}
```

---

### 9. **`options` 섹션**

Pipeline의 실행 동작을 제어

```groovy
options {
    timeout(time: 1, unit: 'HOURS')  // 최대 실행 시간 제한
    timestamps()                    // 콘솔 로그에 타임스탬프 추가
    disableConcurrentBuilds()       // 중복 실행 방지
    skipStagesAfterUnstable()       // 불안정 상태 후 나머지 단계 건너뜀
}

```

---

### 10. **`input` 섹션**

사용자 입력 대기 작업을 정의

```groovy
stage('Approval') {
    steps {
        input {
            message 'Do you want to proceed?'
            ok 'Yes'
        }
    }
}
```

---

### 11. **`tools` 섹션**

빌드 도구를 설정

```groovy
tools {
    maven 'Maven 3.6.3'        // Jenkins에 설치된 Maven 사용
    jdk 'Java 8'               // Jenkins에 설치된 JDK 사용
}
```

---

### 12. **조건부 실행 (`when`)**

특정 조건에 따라 단계를 실행

```groovy
stages {
    stage('Deploy') {
        when {
            branch 'main'         // 특정 브랜치에서만 실행
        }
        steps {
            echo 'Deploying...'
        }
    }
}
```

---

### 13. **`parallel` 섹션**

여러 단계를 병렬로 실행

```groovy
stages {
    stage('Parallel Stage') {
        parallel {
            stage('Test 1') {
                steps {
                    echo 'Running Test 1...'
                }
            }
            stage('Test 2') {
                steps {
                    echo 'Running Test 2...'
                }
            }
        }
    }
}
```


---

### Declarative Pipeline 주요 문법 요약

| 구성 요소         | 역할               | 예시 문법                               |
| ------------- | ---------------- | ----------------------------------- |
| `pipeline`    | Pipeline 전체 구조   | `pipeline { ... }`                  |
| `agent`       | 실행할 노드 정의        | `agent { docker { ... } }`          |
| `stages`      | 주요 단계 정의         | `stages { stage('Build') { ... } }` |
| `steps`       | 각 단계에서 실행할 작업 정의 | `steps { echo 'Building...' }`      |
| `post`        | 후처리 작업 정의        | `post { success { ... } }`          |
| `environment` | 환경 변수 설정         | `environment { VAR = 'value' }`     |
| `parameters`  | 사용자 입력 파라미터 설정   | `parameters { string(...) }`        |
| `triggers`    | 자동 트리거 설정        | `triggers { cron(...) }`            |
| `options`     | 실행 옵션 설정         | `options { timeout(...) }`          |
| `input`       | 사용자 입력 대기        | `input { message '...' }`           |
| `tools`       | 빌드 도구 설정         | `tools { maven '...' }`             |
| `when`        | 조건부 실행           | `when { branch 'main' }`            |
| `parallel`    | 병렬 실행 단계         | `parallel { stage(...) }`           |

---

- # Scripted Pipeline
	- 최상단에 node 지시어로 시작함.

서버 용 Jenkinsfile 예시
- 체크아웃 > 빌드 > 스웨거 배포 > 서버 배포
```bash
pipeline {
    agent any
    triggers {
        // GitHub webhook 트리거
        pollSCM('')
    }
    stages {
        stage('Checkout') {
            steps {
                // GitHub에서 코드 가져오기
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo 'Building project...'
                sh './gradlew clean build'
            }
        }
        stage('Swagger Deploy') {
		    steps {
		        // Swagger JSON을 클라이언트가 접근 가능한 경로에 배포
		        sh 'scp build/swagger-ui/swagger.json user@server:/path/to/swagger'
		    }
		}
        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                sh '''
                    scp build/libs/*.jar user@server:/deploy/path
                    ssh user@server "systemctl restart spring-boot-service"
                '''
            }
        }
    }
    post {
        success {
            echo 'Build and deployment successful!'
        }
        failure {
            echo 'Build or deployment failed!'
        }
    }
}


```


클라이언트 예시
```bash
pipeline {
    agent any
    triggers {
        // GitHub webhook 트리거
        pollSCM('')
    }
    stages {
        stage('Checkout') {
            steps {
                // Git 레포지토리에서 클라이언트 코드 체크아웃
                checkout scm
            }
        }
        stage('Install Dependencies') {
            steps {
                // npm 패키지 설치
                sh 'npm install'
            }
        }
        stage('Build') {
            steps {
                // Vue 앱 빌드
                sh 'npm run build'
            }
        }
        stage('Deploy') {
            steps {
                // 빌드 결과물을 서버에 배포 (경로는 apache나 nginx 위치로)
                sh 'scp -r dist/* user@server:<경로>'
            }
        }
    }
    post {
        success {
            echo 'Build and deployment successful!'
        }
        failure {
            echo 'Build or deployment failed!'
        }
    }
}

```