# 🔄 CI/CD এবং Jenkins 

---

## 📌 CI/CD কী?

**CI/CD** মানে **Continuous Integration / Continuous Delivery (বা Deployment)**।

> এটি এমন একটি পদ্ধতি যেখানে developer-রা code লেখার পরপরই সেটা **automatically build, test এবং deploy** হয়ে যায় — কোনো manual কাজ ছাড়াই।

---

## 🔗 CI — Continuous Integration

| বিষয় | বিবরণ |
|-------|--------|
| **কী করে?** | Developer-রা ঘন ঘন তাদের code একটি shared repository-তে merge করে |
| **কেন দরকার?** | Merge হলেই automatically build ও test চলে |
| **সুবিধা** | Bug দ্রুত ধরা পড়ে, team-এর মধ্যে conflict কমে |

---

## 🚀 CD — Continuous Delivery / Deployment

| বিষয় | বিবরণ |
|-------|--------|
| **কী করে?** | Test পাস করা code automatically staging বা production-এ যায় |
| **কেন দরকার?** | Manual step ছাড়াই দ্রুত software release করা যায় |
| **সুবিধা** | Release দ্রুত হয়, human error কমে |

> 💡 **Delivery vs Deployment পার্থক্য:**
> - **Delivery** → production-এ পাঠানোর জন্য *ready*, কিন্তু একটু manual approval লাগে
> - **Deployment** → সম্পূর্ণ automatic, approval ছাড়াই চলে যায়

---

## 🔄 CI/CD Flow (ধাপে ধাপে)

```
① Developer code লিখল
         ↓
② Git-এ push করল
         ↓
③ CI/CD tool সেটা detect করল
         ↓
④ Automatically build হলো
         ↓
⑤ Tests চললো
         ↓
    ┌────┴────┐
   ✅ PASS   ❌ FAIL
    ↓          ↓
Production  Developer-কে
-এ Deploy   Alert পাঠালো
```

---

## 🛠️ Jenkins কী?

**Jenkins** হলো একটি **open-source automation server** যা CI/CD pipeline তৈরিতে সাহায্য করে।

- Java দিয়ে তৈরি
- সম্পূর্ণ **বিনামূল্যে**
- নিজের server-এ চালানো যায় (self-hosted)
- **১৮০০+ plugin** আছে

---

## ✅ Jenkins দিয়ে যা করা যায়

- Code push হলে **automatically build trigger** করা
- **Unit test, integration test** চালানো
- Code **production server-এ deploy** করা
- **Notification** পাঠানো (Email, Slack, Teams ইত্যাদি)
- **Schedule** করে কাজ চালানো (যেমন: রাত ১২টায় backup)

---

## 📄 Jenkinsfile উদাহরণ

```groovy
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the app...'
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'npm test'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying to production...'
                sh './deploy.sh'
            }
        }
    }

    post {
        success { echo '✅ Build successful!' }
        failure { echo '❌ Build failed! Check the logs.' }
    }
}
```

---

## ⚖️ Jenkins vs অন্যান্য CI/CD টুল

| টুল | হোস্টিং | বিশেষত্ব | কাদের জন্য ভালো |
|-----|---------|----------|-----------------|
| **Jenkins** | Self-hosted | সবচেয়ে flexible, বিশাল plugin ecosystem | Enterprise, বড় team |
| **GitHub Actions** | Cloud | GitHub-এর সাথে built-in, সহজ setup | GitHub user-দের জন্য |
| **GitLab CI** | Cloud/Self | GitLab-এর সাথে integrated | GitLab user-দের জন্য |
| **CircleCI** | Cloud | দ্রুত, সহজ configuration | Startup, ছোট team |
| **Travis CI** | Cloud | Open source project-এ জনপ্রিয় | Open source প্রকল্প |

---

## 🎯 কখন কোনটা বেছে নেবেন?

```
আপনার কাছে নিজের server আছে?
├── হ্যাঁ → Jenkins ব্যবহার করুন
└── না  → Cloud-based টুল বেছে নিন
              ├── GitHub ব্যবহার করেন? → GitHub Actions
              ├── GitLab ব্যবহার করেন? → GitLab CI
              └── অন্যথায় → CircleCI
```

---

## 📚 সারসংক্ষেপ

| বিষয় | মূল কথা |
|-------|---------|
| **CI** | Code merge হলেই automatically build ও test |
| **CD** | Test পাস হলে automatically deploy |
| **Jenkins** | CI/CD চালানোর জনপ্রিয় open-source টুল |
| **সুবিধা** | দ্রুত release, কম bug, কম manual কাজ |

---

> 💬 *আরও জানতে চাইলে: Jenkins installation, Pipeline তৈরি, বা GitHub Actions setup — যেকোনো বিষয়ে জিজ্ঞেস করুন!*
