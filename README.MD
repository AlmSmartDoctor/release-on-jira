# release-on-jira

이 GitHub Action은 Git 태그가 푸시될 때 자동으로 Jira 릴리스를 생성하고 관련된 Jira 티켓을 연결합니다.

## 특징

- Git 태그 푸시 시 자동으로 Jira 릴리스 생성
- 이전 태그와 현재 태그 사이의 커밋 메시지에서 Jira 티켓 번호 추출
- 추출된 티켓을 릴리스에 연결

## 사용 방법

아래 예시와 같이 워크플로우 파일을 작성하세요:

```yaml
name: Release on Jira when Git tag pushed
on:
  push:
    tags:
      - "[0-9]+.[0-9]+.[0-9]+"
jobs:
  create-jira-release:
    runs-on: ubuntu-latest
    steps:
      - name: Create Jira Release
        uses: your-username/jira-release-action@v1
        with:
          jira_email: ${{ secrets.JIRA_EMAIL }}
          jira_token: ${{ secrets.JIRA_TOKEN }}
          jira_subdomain: "your-subdomain"
          jira_project: "your-project-id"  # jira project id can be found at https://{your-jira-subdomain}/rest/api/3/project 
          jira_project_key: "your-project-key"
          release_prefix: "your-release-prefix"
```

## 입력 파라미터

| 파라미터 | 필수 | 기본값 | 설명 |
|----------|------|--------|------|
| `jira_email` | 예 | | Jira 사용자 이메일 |
| `jira_token` | 예 | | Jira API 토큰 |
| `jira_subdomain` | 예 | | Jira 서브도메인 e.g. "smartdoctor" |
| `jira_project` | 예 | | Jira 프로젝트 ID |
| `jira_project_key` | 예 | | Jira 프로젝트 키 |
| `release_prefix` | 아니오 | | 릴리스 이름 접두사 |
| `fallback_tag` | 아니오 | `1.0.0` | 이전 태그가 없을 경우 사용할 대체 태그 |
