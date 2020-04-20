## # Block storage 

#### 1. 시나리오: 고객의 Block storage를 백업하여 로컬(온프리미스)에 저장
전제: OCI의 Block storage는 백업 시 Object storage를 사용하지만 직접 접근해서 조작(다운로드) 할 수 없다. 

#### 2. 해결 방법 개요: Compute Instance의 전체를 백업하여 지정된 Object storage에 저장 후 다운로드 -> Block volume 은 같이 백업 안됨...

2.1 Create Custom Image: 
- 동작중인 Compute Instance에 Block storage를 attach 한다.
- Web console의 Compute>Instances>인스턴스 선택 후 More Actions에서 Create Custom Image 선택하여 Custom Image를 생성해준다.

2.2 Export Image:
- Custom image가 저장될 Object storage bucket 을 생성한다.(Object Storage>Object storage>Create Bucket)
- 생성된 Custom Image를 Compute>Custom Images 메뉴로 가서 확인 후 리스트 항목 오른쪽 버튼을 클릭해 세부 메뉴 중 export를 실행한다
- 기존에 생성한 bucket을 지정하여 export를 수행한다.

2.3 Download:
- Object storage에서 backup을 위해 기존에 생성한 bucket을 선택한다.
- Objects 항목에서 백업된 항목을 찾아 리스트 항목 오른쪽 버튼을 클릭해 Download를 클릭해준다.

** Restore시에는 역순으로 로컬에 저장된 백업된 Custom Image를 Object Storage에 올리고 이를 Compute Instance 생성시에 선택하여 복원하도록 한다.
