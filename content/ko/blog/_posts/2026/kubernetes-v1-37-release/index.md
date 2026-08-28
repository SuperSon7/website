---
layout: blog
title: "쿠버네티스 v1.37: 가르왈(Garhwal)"
date: 2026-08-26
evergreen: true
slug: kubernetes-v1-37-release
author: >
  [쿠버네티스 v1.37 릴리스 팀](https://github.com/kubernetes/sig-release/blob/master/releases/release-1.37/release-team.md)
release_announcement:
  minor_version: "1.37"
  themes:
    - "가르왈(Garhwal)"
---
**편집자:** Arsh Sharma, Christopher Tineo, Kirti Goyal, Sophia Ugochukwu, Swathi Rao, Troy Connor

이전 릴리스와 마찬가지로 [쿠버네티스 v1.37](/releases/1.37/) 릴리스에는 새로운 스테이블(Stable), 베타(Beta), 알파(Alpha) 기능이 포함되었습니다. 고품질 릴리스를 꾸준히 제공할 수 있는 것은 쿠버네티스 개발 주기의 강력함과 활발한 커뮤니티의 지원 덕분입니다.

이번 릴리스는 67개의 개선 사항으로 구성됩니다.
그중 16개는 스테이블로, 23개는 베타로 승격되었고,
27개는 알파 단계에 진입했으며, 1개는 사용 중단 또는 제거 사항입니다.

## 릴리스 테마와 로고

{{< figure src="k8s-v1.37.svg" alt="쿠버네티스 v1.37 가르왈 릴리스 로고: 링갈 공예에서 영감을 받은 직조 테두리가 눈 덮인 히말라야 봉우리, 계단식 밭, 데오다르 나무, 굽이치는 강, 1.37이 표시된 산속 집, 다채로운 깃발, 히말라야 모날, 중앙에 쿠버네티스 조타륜 심볼이 있는 붉은 부란시 꽃을 둘러싸고 있다" class="release-logo" >}}

쿠버네티스 v1.37의 테마는 인도 우타라칸드주의 히말라야 지역인 **가르왈(Garhwal)**(गढ़वाल, _gaṛhvāl_로 발음)입니다. 가르왈 히말라야의 눈 덮인 봉우리, 데오다르 숲, 계단식 밭, 강과 시내, 산길이 지역과 로고의 모습을 함께 빚어냅니다. 이 요소들은 모든 층위와 경로, 기여가 서로 연결된 커뮤니티를 나타냅니다.

로고는 가르왈 풍경을 내다보는 창으로 구상되었습니다.<sup>1</sup> 창 안에서는 계단식 밭이 눈 덮인 봉우리를 향해 올라가며, 각 단은 아래 단의 지지를 받습니다. 이는 모든 쿠버네티스 릴리스가 앞서 이어진 작업에 의존하는 모습과 같습니다. 강은 계곡을 굽이치며 산의 물줄기를 모읍니다. 여러 SIG와 커뮤니티의 기여가 하나의 프로젝트로 흘러드는 모습을 나타냅니다.

데오다르 숲은 서로 다른 프로젝트가 공통의 터전을 공유하며 나란히 성장하는 더 넓은 쿠버네티스 생태계를 나타냅니다. 석공예와 목공예는 길과 산속 집의 형태를 빚어 사람을 중심에 두며, 뒤따르는 이들을 위해 함께 유지하는 기반을 떠올리게 합니다. 강 위에서는 다채로운 깃발이 바람을 받아 풍경에 생기를 더합니다.

장면을 둘러싼 무늬 테두리는 유연한 히말라야 왜성 대나무인 _링갈(ringaal)_로 엮는 바구니 공예에서 영감을 받았습니다. 낱개의 줄이 서로 엮일 때 강해지듯, 코드, 리뷰, 테스트, 문서화, 조율이 하나로 모여 릴리스를 만듭니다.

테두리 안에는 우타라칸드주의 상징 새인 [히말라야 모날](https://en.wikipedia.org/wiki/Himalayan_monal)이 히말라야 고산 지대에 살고 있습니다. 무지갯빛 깃털이 한 번에 여러 색을 품은 모습은 쿠버네티스 커뮤니티가 다양한 기술과 관점을 하나의 프로젝트에 모으는 모습과 닮았습니다. 우타라칸드주의 상징 나무인 붉은 _부란시(buransh)_(_Rhododendron arboreum_) 꽃은 중앙에 쿠버네티스 조타륜을 품어 가르왈의 친숙한 꽃과 커뮤니티가 공유하는 상징을 연결합니다. 집에는 데바나가리 숫자로 1.37을 뜻하는 १.३७이 표시되어 릴리스를 이 풍경에 자리 잡게 합니다.

<sub>1. 창(로고)을 계속 바라보세요. 강이 흐르고 깃발이 바람을 받는 모습을 지켜보세요. 37초가 지나면 풍경이 마법을 드러냅니다. 😉</sub>

## 주요 업데이트 하이라이트

쿠버네티스 v1.37에는 새로운 기능과 개선 사항이 가득합니다. [릴리스 팀](https://github.com/kubernetes/sig-release/blob/master/releases/release-1.37/release-team.md)이 강조하고 싶은 주요 업데이트 몇 가지를 소개합니다!

### 스테이블: 견고한 watch 캐시 초기화

쿠버네티스 v1.37은 _견고한 watch 캐시 초기화_ 작업을 완료합니다.
`ResilientWatchCacheInitialization` 기능 게이트는 v1.34에서 이미 스테이블에 도달했고, v1.37에서는 남아 있던
`WatchCacheInitializationPostStartHook` 게이트가 스테이블로 승격되어 항상 활성화됩니다. 이 게이트는 v1.36부터 기본적으로
활성화되어 API 서버의 시작 및
복구 과정을 더욱 견고하게 만들었습니다. 이제 watch 캐시 초기화와 재초기화는 `etcd`에 요청 트래픽이 급증하게 하지 않으며,
캐시가 준비되는 동안 요청이 쌓이지 않고 안정적으로 처리됩니다.

비용이 큰 list 및 watch 요청이 `etcd`에 과부하를 주거나 API 우선순위와 공정성 용량을 소진하게 두는 대신, 이제 `kube-apiserver`는 제한된 요청을 안전하게 위임하고 나머지는 HTTP 429 응답으로 거부합니다. 이를 통해 대규모 클러스터에서 컨트롤
플레인 장애가 발생할 위험을 줄입니다. 사용자 정의 컨트롤러와 오퍼레이터를 포함한 클라이언트는 `Retry-After` 헤더를 준수하고 지수 백오프를 구현하여 HTTP `429 Too Many Requests` 응답을 안정적으로 처리하도록 설계해야 합니다.

이 작업은 [SIG API Machinery](https://www.kubernetes.dev/community/community-groups/sigs/api-machinery/)가 주도한 [KEP #4568](https://www.kubernetes.dev/resources/keps/4568/)의 일환으로 진행되었습니다.

### 베타: HorizontalPodAutoscaler의 0까지 스케일링

쿠버네티스 v1.37에서 HorizontalPodAutoscaler의 _0까지 스케일링_ 지원이 베타로 승격됩니다. 이 기능은
쿠버네티스 v1.16에서 처음 도입되었으며, 이제 **기본적으로 활성화**됩니다.
오브젝트 또는 외부 메트릭을 사용하는 워크로드의 경우, 이 기능을 통해 HorizontalPodAutoscaler가 유휴 상태일 때 파드 수를
0으로 줄이고 수요가 돌아오면 복원할 수 있습니다. 이를 통해 큐 컨슈머, 배치 잡,
GPU 워크로드의 비용을 줄일 수 있습니다. 워크로드에 `spec.minReplicas: 0`을 설정하면 이 기능이 적용됩니다.

CPU와 메모리 메트릭은 실행 중인 파드에 의존하므로 이를 기반으로 0까지 스케일링하는 기능은 **지원되지 않습니다**.
대신 이 기능은 처리할 작업이 큐에 들어올 때까지 레플리카 수를 0으로 유지하는 경우 등에 적합합니다.

HorizontalPodAutoscaler가 워크로드의 레플리카를 0으로 유지하는 동안
HorizontalPodAutoscaler 상태에 값이 `True`인 `ScaledToZero` 컨디션을 기록합니다. 이후
`HorizontalPodAutoscaler` 컨트롤러는 이 컨디션을 사용해 자신이 0으로 스케일링하여 메트릭이 돌아오면
다시 확장할 워크로드와 레플리카 수를 0으로 설정해 수동으로 비활성화한 워크로드를 구분합니다.
워크로드가 다시 확장되면 컨디션은 사유가 `NotScaledToZero`인 `False`로 설정됩니다.

이 작업은 [SIG Autoscaling](https://www.kubernetes.dev/community/community-groups/sigs/autoscaling/)이 주도한 [KEP #2021](https://www.kubernetes.dev/resources/keps/2021/)의 일환으로 진행되었습니다.

### 베타: 매니페스트 기반 어드미션 제어 구성

쿠버네티스 v1.37에서 [매니페스트 기반 어드미션 제어](/docs/reference/access-authn-authz/manifest-admission-control/)
구성이 베타로 승격됩니다. 이제 어드미션 웹훅과 CEL 기반 정책을 쿠버네티스 API에만 두지 않고,
`AdmissionConfiguration`의 `staticManifestsDir` 필드를 통해 디스크의 매니페스트 파일에서 불러올 수 있습니다. 이 방식으로 불러온 정책은
API 서버 시작 시점부터 적용되고 `etcd`를 사용할 수 없는 동안에도 계속 작동하며, API 기반 어드미션
리소스 자체가 변경되지 않도록 보호할 수 있습니다.

이 작업은 [SIG API Machinery](https://www.kubernetes.dev/community/community-groups/sigs/api-machinery/)가 주도한 [KEP #5793](https://www.kubernetes.dev/resources/keps/5793/)의 일환으로 진행되었습니다.

### 알파: 파드 단위 체크포인트 및 복원

쿠버네티스 v1.37은 **파드 단위** 체크포인트 및 복원에 대한 알파 지원을 도입합니다.
CRI에 `CheckpointPod`와 `RestorePod` RPC를 추가하여 kubelet과 호환되는 컨테이너 런타임이 파드 체크포인트를 만들고 이 체크포인트에서 파드를 복원할 수 있게 합니다.
이 기능을 사용하려면 컨테이너 런타임도 이 새로운 RPC를 구현해야 합니다.

이 작업은
[SIG Node](https://www.kubernetes.dev/community/community-groups/sigs/node/)가 주도한 [KEP #5823](https://www.kubernetes.dev/resources/keps/5823/)의 일환으로 진행되었습니다.

## 스테이블로 승격된 기능

여기에는 스테이블(일반적으로 사용 가능(General Availability)이라고도 함)로 승격된 모든 기능을 나열합니다. 알파에서 베타로 승격된 기능과 신규 기능을 포함한
전체 업데이트 목록은 릴리스 노트를 참고합니다.

이번 릴리스에서 총 16개의 개선 사항이 스테이블로 승격되었습니다.

### KYAML

_KYAML_은 쿠버네티스를 위해 특별히 설계된, 더 안전하고 모호함이 적은 YAML 하위 집합이며 **YAML을 대체하지 않습니다**. 모든
KYAML 파일은 유효한 YAML이므로 모든 버전의 `kubectl`에 KYAML을 입력할 수 있으며, 입력을 파싱하기 위해 명세 파일을
KYAML로 작성할 필요가 없습니다. 기존 매니페스트, 도구, 파이프라인을 변경할 필요도 없습니다.
v1.34에서 알파로 도입되고 v1.35에서 베타로 승격된 KYAML은 적합성
테스트를 완료하여 v1.37에서 스테이블로 승격되며, `kubectl get -o kyaml`도 이제 스테이블입니다.

KYAML에 대해 자세히 알아보려면 [쿠버네티스 YAML을 KYAML로 보기 좋게 출력하는 방법과 그 이유](/blog/2026/08/11/how-to-pretty-print-kubernetes-yaml-as-kyaml/)를 확인합니다.

이 작업은 [SIG CLI](https://www.kubernetes.dev/community/community-groups/sigs/cli/)가 주도한 [KEP #5295](https://www.kubernetes.dev/resources/keps/5295/)의 일환으로 진행되었습니다.

### metrics.k8s.io API

_metrics.k8s.io_ API는 약 9년 동안 베타로 유지된 뒤 쿠버네티스 v1.37에서 스테이블로 승격됩니다. 이 API는 파드와 노드의
CPU 및 메모리 사용량을 조회하는 표준 방식을 제공하며,
HorizontalPodAutoscaler(HPA)와 `kubectl top` 같은 명령 등 널리 사용되는 쿠버네티스 기능을 지원합니다.

이번 승격은 베타 API를 영구히 유지하지 않으려는 쿠버네티스 프로젝트의 목표에 따른 것입니다. 이제 `v1`이 존재하므로 이후
쿠버네티스 릴리스는 이를 사용하도록 전환합니다. `v1beta1`은 API
사용 중단 정책에 따라 전환 기간 내내 사용할 수 있으므로, 기존 워크플로를 중단하지 않고 스테이블 API를 도입할 수 있습니다.

이 작업은
[SIG Instrumentation](https://www.kubernetes.dev/community/community-groups/sigs/instrumentation/)이 주도한 [KEP #5207](https://www.kubernetes.dev/resources/keps/5207/)의 일환으로 진행되었습니다.

### `SELinuxMount`와 `SELinuxChangePolicy`

쿠버네티스 v1.37에서 `SELinuxMount`와 `SELinuxChangePolicy` 플래그가 스테이블에 도달하여 기본적으로 활성화됩니다. 이는
볼륨에 재귀적으로 레이블을 다시 지정하는 대신 `-o context=<label>`(MountOption 기본값)로 마운트한다는 뜻이지만,
볼륨의 CSI 드라이버가 CSI드라이버(CSIDriver) 오브젝트에서 `.spec.seLinuxMount: true`를 설정해 이 기능을 사용하도록 선택한 경우에만 적용됩니다.

하나의 마운트는 하나의 SELinux 컨텍스트만 가질 수 있으므로, [같은 노드에서 서로 다른 SELinux 레이블을 사용하는 파드가 볼륨을 공유하면
재귀적 레이블 재지정에서는 함께 실행되던 파드가 이제 시작되지 않을 수 있습니다](https://www.kubernetes.dev/resources/keps/1710/#story-3-cluster-upgrade).
워크로드에서 이전 동작을 유지하려면 파드의 `.spec.seLinuxChangePolicy`를 `Recursive`로 설정하는 것이 좋습니다.

이 동작 자체는 v1.38까지 고정되지 않으므로, 한 번의 릴리스 동안은 클러스터 전체에서 비활성화할 수 있습니다.

SELinux가 활성화되지 않은 클러스터에는 아무런 영향이 없습니다. 자세한 내용은 [SELinux 볼륨 레이블 변경 사항의 GA 승격(및
v1.37에서 예상되는 영향)](/blog/2026/04/22/breaking-changes-in-selinux-volume-labeling/)을 확인합니다.

이 작업은 [SIG Storage](https://www.kubernetes.dev/community/community-groups/sigs/storage/)가 주도한 [KEP #1710](https://www.kubernetes.dev/resources/keps/1710/)의 일환으로 진행되었습니다.

### 스테이블로 승격된 DRA 기능

#### DRA: 표준화할 수 있는 네트워크 인터페이스 데이터를 포함한 ResourceClaim 상태

ResourceClaim의 `.status.devices`가 쿠버네티스 v1.37에서 스테이블에 도달하여, 드라이버가 리소스 클레임에 할당된 각 장치의
장치별 상태 데이터를 보고할 수 있습니다. 이를 통해 장치 구성 방식을 더 쉽게 확인하고,
문제를 해결하며, 다른 서비스와 함께 장치를 사용할 수 있습니다.

이 기능은 네트워크 장치에 특히 유용합니다. 이 필드가 추가되기 전에는 파드가 DRA를 통해 네트워크 장치를 요청했을 때,
시스템의 다른 컴포넌트가 해당 네트워크 장치에 할당된 IP 주소를 알 방법이 없었습니다.
새 상태 필드는 DRA 드라이버가 필요한 컴포넌트에 이 정보를 내보내는 표준 방식을 제공하여,
DRA로 보조 네트워크 인터페이스를 파드에 연결하는 기능을 온전히 사용할 수 있게 합니다.

이 작업은 [SIG Node](https://www.kubernetes.dev/community/community-groups/sigs/node/)와 [SIG Network](https://www.kubernetes.dev/community/community-groups/sigs/network/)가 주도한 [KEP #4817](https://www.kubernetes.dev/resources/keps/4817/)의 일환으로 진행되었습니다.


#### DRA: DRA 드라이버를 통한 확장 리소스 요청 처리

DRA 확장 리소스 지원이 쿠버네티스 v1.37에서 스테이블에 도달합니다. 이 기능을 통해 DRA 드라이버는 파드 명세의
`abc.example/gpu: 3`과 같은 기존 _확장 리소스_ 메커니즘으로 생성된 요청을 별도의
[장치 플러그인](/docs/concepts/extend-kubernetes/compute-storage-net/device-plugins/) 없이 처리할 수 있습니다.

이 메커니즘을 사용하면 확장 리소스 이름을 DeviceClass에 직접 할당할 수 있습니다. 그러면 해당 리소스를 요청하는 파드는 워크로드에 ResourceClaim을 정의하지 않아도 DRA를 통해 장치를 할당받을 수 있습니다.

이 작업은 [SIG Scheduling](https://www.kubernetes.dev/community/community-groups/sigs/scheduling/)이 주도한 [KEP #5004](https://www.kubernetes.dev/resources/keps/5004/)의 일환으로 진행되었습니다.

#### DRA: 장치 테인트(taint)와 톨러레이션(toleration)

DRA로 관리하는 물리 장치의 _테인트와 톨러레이션_ 지원이 쿠버네티스 v1.37에서 스테이블에 도달했습니다. 기본적으로 사용 가능한 모든 장치를 스케줄링 대상으로 고려할 수 있습니다. 이 개선 사항을 통해 DRA 드라이버가 특정 장치를 테인트하여 워크로드에 선택되지 않도록 함으로써 장치 스케줄링을 더욱 세밀하게 제어할 수 있습니다. 또는 클러스터 관리자가 특정 드라이버에서 관리하는 모든 장치와 같은 특정 선택 기준에 따라 장치를 테인트하는 DeviceTaintRule을 만들 수 있습니다.

이 작업은 [KEP #5055](https://www.kubernetes.dev/resources/keps/5055/)의 일환으로 진행되었으며,
[SIG Scheduling](https://www.kubernetes.dev/community/community-groups/sigs/scheduling/)이 주도했습니다.

#### DRA: 표준 numaNode 장치 속성 {#dra-standard-numanode-device-attribute}

쿠버네티스 v1.37은 새로운 표준 _NUMA 노드 장치 속성_을 정의합니다. 이 기능은
`resource.kubernetes.io/numaNode`를 장치의 NUMA 노드 정보를 나타내는 공용 속성 이름으로 표준화하여,
서로 다른 DRA 드라이버가 관리하는 장치를 같은 NUMA 노드를 기준으로 비교할 수 있게 합니다. 각 드라이버가 자체 속성 이름을 정의하지 않아도 되며,
여러 장치에서 NUMA 배치를 식별하는 일관된 방식을 제공합니다. 이 개선 사항은 기능 게이트나 트리 내부 동작 변경이 없는
명명 및 등록 KEP이므로 바로 스테이블로 도입됩니다.

이 작업은 [SIG Node](https://www.kubernetes.dev/community/community-groups/sigs/node)가 주도한 [KEP #6072](https://www.kubernetes.dev/resources/keps/6072/)의 일환으로 진행되었습니다.

### 노드 선언 기능 {#node-declared-features}

_노드 선언 기능_은 쿠버네티스 v1.37에서 스테이블로 승격되어, 노드에서 기능 게이트로 제어되는 특정 쿠버네티스 기능을 사용할 수 있는지 선언하는 프레임워크를 제공합니다.
이 정보는 이후 `kube-scheduler`, 어드미션 컨트롤러, API 서버 자체와 같은 컨트롤 플레인 컴포넌트가 버전 차이(skew)를 관리하는 데 사용됩니다.

이 기능은 노드에 새로운 `.status.declaredFeatures` 필드를 도입하여 알파 → 베타 → 스테이블 단계를 거쳐
승격되는 기능을 선언하는 데 사용합니다. 컨트롤 플레인은 서로 다른 노드 버전이 섞여 실행되는 클러스터에서도 이 정보를 사용해
올바른 동작을 적용할 수 있습니다.

기능이 스테이블로 승격되고 지원되는 버전 차이 범위의 모든 노드가 이를 지원한다고 컨트롤 플레인이 간주할 수 있게 되면
노드는 해당 기능 보고를 중단합니다.

`kubelet`은 시작할 때 기능 게이트와 노드의 정적
구성만을 기반으로 선언 기능을 결정합니다. 따라서 변경 사항을 적용하려면 `kubelet`을 다시 시작해야 합니다.

이 작업은 [SIG Node](https://www.kubernetes.dev/community/community-groups/sigs/node/)가 주도한 [KEP #5328](https://www.kubernetes.dev/resources/keps/5328/)의 일환으로 진행되었습니다.

### 스토리지 버전 마이그레이터 {#storage-version-migrator}

쿠버네티스 v1.37에서는 _StorageVersionMigration API_(`storagemigration.k8s.io/v1`)가 스테이블로 승격되어 기본적으로
활성화됩니다. 이 API는 선호 스토리지 버전이 `v1beta1`에서 `v1`로 변경되는 경우처럼 API 업그레이드 후 기존의 내장 및 사용자 정의 리소스를 이전 스토리지 버전에서 새 스토리지
버전으로 마이그레이션하는 데 도움이 됩니다. 또한 저장 데이터 암호화 설정이 변경된 뒤 기존
데이터를 다시 작성하여 오래된 데이터를 새 암호화 설정으로 저장하는 데도 사용할 수 있습니다.

과거에는 클러스터 관리자와 CustomResourceDefinition 작성자가 기존 리소스를 다시 작성하려면 수동 `kubectl get` 또는
`kubectl replace` 스크립트를 사용하거나 트리 외부 `kube-storage-version-migrator` 컴포넌트를 배포해야 했습니다. 이러한
방식은 대개 번거롭고 오류가 발생하기 쉬우며 모니터링하기 어려웠습니다.

스토리지 버전 마이그레이션을 시작하려면 사용자가 선언적 StorageVersionMigration 오브젝트를 생성해야 합니다. 쿠버네티스 컨트롤 플레인의 내장
`StorageVersionMigrator` 컨트롤러는 이 오브젝트를 감시하고 기존 리소스를 해당 API의 기본 스토리지 버전으로 자동 마이그레이션합니다.
StorageVersionMigration은 표준 쿠버네티스 API이므로
CRD 작성자는 마이그레이션을 별도로 관리하는 대신 CRD 업그레이드의 일부로 실행할 수 있습니다.

이 작업은 [SIG API Machinery](https://www.kubernetes.dev/community/community-groups/sigs/api-machinery/)가 주도한 [KEP #4192](https://www.kubernetes.dev/resources/keps/4192/)의 일환으로 진행되었습니다.

### 스테이블: 파드 인증서와 클러스터 트러스트 번들 {#pod-certificates-and-clustertrustbundles}

[파드 인증서](/docs/reference/access-authn-authz/certificate-signing-requests/#pod-certificate-requests)와 밀접하게 관련된 [ClusterTrustBundles](/docs/reference/access-authn-authz/certificate-signing-requests/#cluster-trust-bundles)가
모두 쿠버네티스 v1.37에서 스테이블로 승격되어 개인 키, X.509
인증서, 트러스트 번들을 파드에 배포하는 일급 지원을 제공합니다.

이를 사용하려면 개발자 또는 관리자가 서명자 이름을 선택하고
PodCertificateRequest 오브젝트를 감시하여 대상 파드의 인증서를 발급하고 갱신하며, 인증서 검증에 필요한 트러스트 앵커가 포함된 해당 ClusterTrustBundle 오브젝트를 유지 관리하는 _서명자 컨트롤러_를 배포합니다.
그런 다음 워크로드는 선택한 서명자 이름으로 `podCertificate` 프로젝티드 볼륨을 정의하여 이 아이덴티티를 사용하도록 선택합니다. 워크로드는 ClusterTrustBundle 프로젝티드 볼륨을 마운트해 트러스트 앵커 정보를 불러올 수도 있습니다.

이 작업은 [SIG Auth](https://www.kubernetes.dev/community/community-groups/sigs/auth/)가 주도한 [KEP #4317](https://www.kubernetes.dev/resources/keps/4317/)과 [KEP #3257](https://www.kubernetes.dev/resources/keps/3257/), 두 KEP의 일환으로 진행되었습니다.

## 베타로 승격된 기능

### 쿠버네티스의 갱 스케줄링 지원

쿠버네티스가 대규모 AI/ML 워크로드 관리의 사실상 표준이 되면서 AI/ML 훈련 잡과 HPC 시뮬레이션 같은 워크로드를 스케줄링하는 일이 그 어느 때보다 중요해졌습니다. 하지만 기본 쿠버네티스 스케줄러는 파드를 개별적으로 스케줄링하므로 일부 파드는 스케줄링되는 반면 다른 파드는 리소스 부족으로 대기 상태에 머물 수 있어 스케줄링이 어렵습니다. 이러한 부분 스케줄링은 교착 상태와 비효율적인 클러스터 리소스 사용으로 이어질 수 있습니다.

_갱 스케줄링(gang scheduling)_은 쿠버네티스 v1.37에서 베타로 승격되어 Workload API와 PodGroup 개념을 통한 네이티브 갱 스케줄링 지원을 개선합니다.
이 기능은 _전부 아니면 전무(all-or-nothing)_ 스케줄링 전략을 구현하여, 정의된 파드 그룹 전체를 수용할 충분한 리소스가 클러스터에 있을 때만 스케줄링되도록 보장합니다. 이 개선 사항의 베타 승격은 워크로드 진행에 도움이 되지 않는 성급한 선점을 피하는 워크로드 인지 선점과, 경합하는 워크로드를 더 잘 조율하는 PodGroup 큐잉도 도입합니다.

특히 `kube-scheduler`가 여러 워크로드를 동시에 스케줄링할 때 서로 반복적으로 방해하면서 진척을 내지 못하는 라이브락 시나리오를 해결합니다.

이 작업은 [SIG Scheduling](https://www.kubernetes.dev/community/community-groups/sigs/scheduling/)이 주도한 [KEP #4671](https://www.kubernetes.dev/resources/keps/4671/)의 일환으로 진행되었습니다.


### 쿠버네티스 메트릭의 네이티브 히스토그램 지원

쿠버네티스는 컨트롤 플레인 컴포넌트 전반에서 [프로메테우스 형식](https://prometheus.io/docs/instrumenting/exposition_formats/)으로 수백 개의 히스토그램 메트릭을 노출하며, 이는
클러스터 상태를 모니터링하고 성능 문제를 디버깅하는 데 필수적입니다. 하지만 기존 프로메테우스 히스토그램은 사전에 정의된 정적
버킷에 의존하므로 데이터 정확도와 메모리 사용량 사이에서 절충해야 했습니다. 이를 완화하기 위해 프로메테우스는 고정된 경계 대신 동적인 지수 버킷 경계를 사용하는 _네이티브
히스토그램_을 도입했습니다. 네이티브 히스토그램은
기존 모니터링 인프라와 완전한 하위 호환성을 유지하면서
스토리지 효율을 크게 높이고 쿼리 성능을 개선하며 분포를 더 세밀하게 보여줍니다.

쿠버네티스 v1.37은 쿠버네티스 메트릭의 네이티브 히스토그램 지원을 베타로 승격합니다. `NativeHistograms` 기능 게이트를 도입한
알파 구현을 기반으로, 베타 단계에서는 구현과 롤아웃 경험을 개선합니다.
이 기능을 활성화하면 요청된 스크랩 프로토콜이 네이티브 히스토그램을 지원할 때 쿠버네티스 컴포넌트가 기존 형식과 네이티브 형식 모두로 히스토그램을 노출합니다.
네이티브 히스토그램, 구체적으로 `PrometheusProto`를 사용하는 경우
기존 대시보드와 경고가 계속 작동하므로 사용자가
자신의 속도에 맞춰 마이그레이션할 수 있습니다. 또한 `init()` 함수에서 생성된 히스토그램이 지연 초기화를 사용하도록 리팩터링하여,
기능 게이트 파싱 후 네이티브 히스토그램 옵션이 올바르게 적용되도록 했습니다. 이러한 변경 사항은 기능 게이트 또는
프로메테우스 3.x 사용자를 위한 프로메테우스 측 구성을 통해 안전하게 롤아웃하고 롤백할 수 있게 하면서 구현의 신뢰성을 높입니다.

이 작업은 [SIG Instrumentation](https://www.kubernetes.dev/community/community-groups/sigs/instrumentation/)이 주도한 [KEP #5808](https://www.kubernetes.dev/resources/keps/5808/)의 일환으로 진행되었습니다.

### WAS: 베타로 승격된 기능

#### 워크로드 인지 선점

쿠버네티스는 전통적으로 파드 단위로 선점을 수행하므로, 긴밀하게 결합된 여러
파드로 구성된 워크로드에는 비효율적일 수 있습니다. 쿠버네티스 v1.37에서 워크로드 인지 선점이 베타로 승격되어 스케줄러가
선점 결정을 내릴 때 PodGroup을 고려할 수 있습니다. 이를 통해 스케줄러는 우선순위가 낮은
워크로드를 선점할 때 워크로드 전체를 고려하여, 워크로드가 진행할 충분한 용량을 확보하지 못하면서 개별 파드만
중단되는 경우를 줄입니다.

이 작업은 [SIG Scheduling](https://www.kubernetes.dev/community/community-groups/sigs/scheduling/)이 주도한 [KEP #5710](https://www.kubernetes.dev/resources/keps/5710/)의 일환으로 진행되었습니다.

#### DRA: 워크로드를 위한 ResourceClaim 지원

동적 리소스 할당(DRA)을 사용하면 파드가 ResourceClaim을 통해 특수 리소스를 요청할 수 있습니다. 쿠버네티스 v1.37에서는
워크로드를 위한 DRA ResourceClaim 지원이 베타로 승격되어 Workload 및 PodGroup API가
ResourceClaim과 ResourceClaimTemplate을 파드 그룹에 연결할 수 있습니다. 이를 통해 ResourceClaim을 각 파드에
개별적으로 예약하지 않고 워크로드 전체에서 공유할 수 있으며, ResourceClaimTemplate은 PodGroup의 클레임을
자동으로 생성할 수 있습니다.

이 작업은 [SIG Scheduling](https://www.kubernetes.dev/community/community-groups/sigs/scheduling/)이 주도한 [KEP #5729](https://www.kubernetes.dev/resources/keps/5729/)의 일환으로 진행되었습니다.

### cAdvisor 없이 CRI만 사용하는 컨테이너 및 파드 통계 {#cadvisor-less-cri-full-stats}

`kubelet`은 전통적으로 `cAdvisor`에서 컨테이너 및 파드 통계를 가져왔고, 컨테이너 런타임
인터페이스(CRI)도 자체 통계를 제공합니다. 동일한 메트릭에 두 가지 소스가 있으면 특정
값의 출처를 파악하기 어렵습니다.

쿠버네티스 v1.37에서는 cAdvisor 없이 CRI만 사용하는 컨테이너 및 파드 통계 개선 사항이 베타로 승격됩니다. 이 개선 사항은
쿠버네티스에 필요한 컨테이너 및 파드 통계를 제공하도록 CRI를 확장하여, `kubelet`이 이러한 메트릭을
`cAdvisor`에 의존하지 않고 컨테이너 런타임에서 직접 가져올 수 있게 합니다.

이를 통해 컨테이너 및 파드 메트릭을 단일 정보 소스로 통합하고, 중복 메트릭 수집을 줄이며
`kubelet`이 통계를 수집하고 노출하는 방식을 간소화합니다.

이 기능은 v1.37에서 베타이지만 기본적으로 **비활성화**되어 있습니다. 사용하려면 `PodAndContainerStatsFromCRI` 기능 게이트를 활성화합니다.

이 작업은 [SIG Node](https://www.kubernetes.dev/community/community-groups/sigs/node/)가 주도한 [KEP #2371](https://www.kubernetes.dev/resources/keps/2371/)의 일환으로 진행되었습니다.

### cgroups v2를 통한 메모리 QoS 지원

쿠버네티스는 쿠버네티스 워크로드의 메모리 보호와 격리를 포괄하도록 서비스 품질 메커니즘을 개선하고 있습니다. 리눅스를 실행하는 노드에서 _메모리
QoS_ 기능은 메모리 요청과 한도(limit)를 사용해 요청한 메모리가 회수되지 않도록 보호하고 워크로드가 하드 한도에 도달하기 전에 메모리 사용을 제한하는 cgroup 제어를 구성합니다. 이를 통해
메모리 압박이 메모리에 민감한 워크로드에 미치는 영향을 줄이고 노드 안정성을 높일 수 있습니다.

쿠버네티스 v1.37에서 메모리 QoS 지원이 베타로 승격됩니다. 이 기능은 `memory.min`,
`memory.low`, `memory.high` 같은 cgroups v2 메모리 제어를 사용해 다양한 수준의 메모리 보호 및 제한을 제공합니다. 예를 들어 메모리 요청을
사용해 메모리가 회수되지 않도록 보호하고, `memory.high`를 사용해 구성된
임계값을 초과하는 워크로드를 제한할 수 있습니다.

`MemoryQoS` 기능 게이트는 v1.37에서 기본적으로 활성화됩니다. 클러스터 운영자는 `kubelet`의
`memoryReservationPolicy` 설정으로 메모리 보호를 제어하고 `memoryThrottlingFactor`로 메모리 제한을 구성할 수 있습니다. 기본값은
v1.37로 업그레이드할 때 기존 워크로드에 예상치 못한 메모리 제한을 도입하지 않으면서, 운영자가
추가 메모리 보호 기능을 사용하도록 선택할 수 있게 설계되었습니다.

이 작업은 [SIG Node](https://www.kubernetes.dev/community/community-groups/sigs/node/)가 주도한 [KEP #2570](https://www.kubernetes.dev/resources/keps/2570/)의 일환으로 진행되었습니다.

### 파드 단위 리소스 관리자

쿠버네티스 v1.37에서 _파드 단위 리소스 관리자_가 `PodLevelResourceManagers` 기능 게이트 뒤에서 베타로 승격됩니다.

이 기능 게이트는 **기본적으로 비활성화**되어 있습니다. 활성화하면 토폴로지, CPU, 메모리 리소스

관리자가 할당 및 NUMA 정렬을 결정할 때 파드 전체에 정의된 리소스를

사용할 수 있습니다. 이를 통해 파드 안의 컨테이너마다 서로 다른 리소스 요구 사항을 계속 지원하면서
파드를 하나의 리소스 단위로 관리할 수 있습니다.

파드 단위 리소스 관리를 사용하면 파드가 전체 리소스 예산에 따라 NUMA에 정렬된 CPU 및 메모리 풀을 예약할 수 있습니다. 전용 리소스가 필요한 컨테이너는 풀에서 배타적인 부분을 할당받고, 사이드카나 보조 워크로드 같은 다른 컨테이너는 나머지 리소스를 공유할 수 있습니다. 이 기능은 동일한 NUMA 노드에서 리소스를 서로 가깝게 유지하면 파드의 모든 컨테이너에 전용 리소스를 할당하지 않고도 성능을 높일 수 있는 AI/ML 및 고성능 컴퓨팅 같은 성능 민감형 워크로드에 특히 유용합니다.

또한 이 기능은 컨테이너가 독립적으로 NUMA에 정렬된 리소스를 계속 할당받을 수 있는 컨테이너 범위를 지원합니다. 이를 통해 성능에 민감한 컨테이너와 리소스 요구 사항이 다른 컨테이너를 조합하는 워크로드에 더 큰 유연성을 제공합니다.

이 작업은 [SIG Node](https://www.kubernetes.dev/community/community-groups/sigs/node/)가 주도한 [KEP #5526](https://www.kubernetes.dev/resources/keps/5526/)의 일환으로 진행되었습니다.

### watch 기반 라우트 컨트롤러 조정

cloud-controller-manager 라이브러리의 라우트 컨트롤러는 이전에 기본 10초의 고정된 주기로 라우트를 조정했습니다. 이 때문에 변경 사항이 없어도 인프라 제공자에 불필요한 요청이 발생하고 새 노드가 추가되었을 때 라우트 업데이트가 지연될 수 있었습니다.

_watch 기반 라우트 컨트롤러 조정_이 쿠버네티스 v1.37에서 베타로 승격되었습니다. 이번 릴리스는 이 작업의 가시성도 추가합니다. 라우트 컨트롤러의 알파 `route_sync_total` 메트릭에 `trigger`(`periodic` 또는 `node_change`)와 `outcome`(`changed`, `noop`, `error`)이라는 두 레이블이 추가되어, 운영자는 주기적 조정이 실제로 라우트 드리프트를 수정하는지 아니면 아무 작업 없이 실행되는지 확인하고 조정 실패를 추적할 수 있습니다.

watch 기반 라우트 컨트롤러 조정을 사용하면 라우트 컨트롤러가 다음 고정 주기를 기다리는 대신 watch 이벤트에 따라 라우트를 조정할 수 있습니다. 노드가 추가 또는 제거되거나 주소 또는 할당된 파드 CIDR이 변경되는 등 관련 노드 변경이 발생하는 즉시 조정을 시작할 수 있습니다. 오래된 라우트를 찾아 상태 일관성을 유지하기 위해 빈도가 낮은 주기적 조정도 계속 실행됩니다. 이 동작은 `CloudControllerManagerWatchBasedRoutesReconciliation` 기능 게이트로 제어되며 기본적으로 비활성화되어 있으므로, 이번 전환은 기본 동작을 바꾸지 않았습니다.

이를 통해 인프라 제공자에 보내는 불필요한 요청을 줄이는 동시에 새로 추가된 노드의 라우트를 더 빨리 조정할 수 있습니다. 변경되는 것은 조정 실행 시점이며, 라우트 조정 로직 자체는 바뀌지 않습니다.

이 작업은 [SIG Cloud Provider](https://www.kubernetes.dev/community/community-groups/sigs/cloud-provider/)가 주도한 [KEP #5237](https://www.kubernetes.dev/resources/keps/5237/)의 일환으로 진행되었습니다.

### 노드의 스토리지 용량 점수

`VolumeBinding` 스케줄러 플러그인은 항상 여유 용량을 기준으로 정적으로 바인딩된 PV의 노드 점수를 계산할 수 있었지만, 이 점수 계산은 동적 프로비저닝에는 적용되지 않았습니다.

CSI 드라이버가 요청에 따라 새 볼륨을 프로비저닝할 때 스케줄러는 여유 공간이 더 많거나 적은 노드를 선호할 방법이 없었습니다.

이는 로컬 스토리지에서 문제가 되었습니다. 관리자는 이후 볼륨 확장을 위한 공간을 남겨두기 위해 여유 용량이 가장 많은 노드에 파드를 배치하거나, 워크로드를 빈패킹하여 클라우드 클러스터에 필요한 노드 수를 줄이기 위해 충분한 용량을 갖춘 노드 중 여유 용량이 가장 적은 노드에 파드를 배치하고 싶을 수 있습니다.

쿠버네티스 v1.37에서는 동적 프로비저닝을 위한 스토리지 용량 점수 기능이 `StorageCapacityScoring`
기능 게이트 뒤에서 베타로 승격됩니다. 이 기능은 v1.33에서 알파로 처음 도입되었으며, [KEP #1845](https://www.kubernetes.dev/resources/keps/1845/)의 기존
`VolumeCapacityPriority` 게이트를 통합하고 사용 중단합니다. 기능을 활성화하면
VolumeBinding 플러그인의 `Score` 확장 지점이 드라이버의 외부
프로비저너 사이드카에서 게시한 `CSIStorageCapacity` 오브젝트를 읽고, 정적 바인딩과 같은 방식으로 동적 프로비저닝의 노드 점수를 계산합니다. 관리자는
`VolumeBindingArgs`의 `Shape` 설정으로 전략을 선택하며, 기본값은 이후 확장을 위한
공간을 남기는 "할당 가능 용량이 최대인 노드 선호"입니다.

이 기능은 오직 `StorageCapacityScoring` 게이트에만 의존합니다. 정적으로
바인딩된 PV의 점수 계산은 CSI 드라이버와 관계없이 기능을 활성화하는 즉시 실행됩니다. 드라이버는 동적으로 프로비저닝된 볼륨에도 용량 인지 점수 계산을 적용하려면
`CSIDriver` 오브젝트에서 `StorageCapacity: true`만 설정하면 됩니다. 이 기능은 완전히
되돌릴 수 있으며, 게이트를 비활성화하면 이미 스케줄링된 파드에는 영향을 주지 않고 정적 및 동적 VolumeBinding 용량 점수 계산을 모두
중단합니다.

이 작업은 [SIG Storage](https://www.kubernetes.dev/community/community-groups/sigs/storage/)가 주도한 [KEP #4049](https://www.kubernetes.dev/resources/keps/4049/)의 일환으로 진행되었습니다.

### CSI 볼륨 연결 한도와 클러스터 오토스케일러 통합

쿠버네티스 v1.37은 CSI 볼륨 연결 한도와 클러스터 오토스케일러의 통합을 개선하여, 대기 중인
파드를 위해 새 노드를 만들 때 CSI 볼륨을 사용하는 모든 대기 파드를 연결하는 데 필요한 새 노드 수를
더 정확히 판단할 수 있게 합니다. 클러스터 오토스케일러는 기존
노드의 CSI 볼륨 연결 한도는 이미 확인할 수 있었지만, 곧 생성할 노드의 한도는 알 수 없었습니다. 이 때문에 스케일 업 규모를 작게 잡아 용량을 추가한 후에도 볼륨 기반
파드가 대기 상태에 남을 수 있었습니다. 스케줄링 측에서는 문제가 더 커집니다. `NodeVolumeLimits` 플러그인은 게시된 CSI 드라이버 정보가 없는 노드에 한도가 전혀 없는 것으로 간주하므로, 아직 `CSINode` 오브젝트를 보고하지 않은 새 노드에는 실제로 마운트할 수 있는 수보다 많은 볼륨 기반 파드가 몰릴 수 있습니다. 이는 지금까지 클러스터 관리자가 해소할 방법이 없던 경쟁 조건입니다.

쿠버네티스 v1.37에서는 CSI 인지 오토스케일링이 `VolumeLimitScaling` 기능 게이트 뒤에서 베타로 승격됩니다. 이 기능은 v1.35에서 알파로 처음 도입되었습니다. 이제 클러스터 오토스케일러는 템플릿화된 `CSINode` 오브젝트를 대상으로 스케일 업 시뮬레이션을 실행하므로, 기존 노드 그룹을 확장하든 0에서 확장하든 연결 한도를 올바르게 계산합니다. 스케줄러 측에서 관리자는 `CSIDriver`별로 새로운 `PreventPodSchedulingIfMissing` 필드를 통해 이 기능을 사용하도록 선택해, 아직 드라이버를 보고하지 않은 노드에 파드가 배치되지 않도록 할 수 있습니다. 전용 `CSIDriverMissingOnNode` 및 `CSINodeMissing` 오류를 통해 이러한 스케줄링 실패를 더 쉽게 디버깅할 수 있습니다. 베타 단계에서는 스케일 다운 동작과 CSI 옵트인 시나리오를 위한 e2e 테스트를 추가하고, CSI 드라이버 정보를 포함하도록 `failed_scale_ups_total` 및 `scaled_up_nodes_total` 메트릭을 업데이트합니다. 오토스케일러와 스케줄러 변경 사항은 모두 엄격하게 옵트인 방식입니다. 기능 게이트를 비활성화하면 `CSINode` 데이터가 없는 노드에 파드를 무제한 배치하는 현재 기본 동작이 복원되므로, 아직 CSI를 인식하지 못하는 오토스케일러(예: Karpenter)를 실행하는 배포판과 관리자가 새 동작을 강제로 적용받지 않습니다.

이 작업은 [SIG Autoscaling](https://www.kubernetes.dev/community/community-groups/sigs/autoscaling/)이 주도한 [KEP #5030](https://www.kubernetes.dev/resources/keps/5030/)의 일환으로 진행되었습니다.

### PVC의 마지막 사용 시각 보고

`PersistentVolumeClaims`는 이를 생성한 워크로드보다 오래 남는 경향이 있습니다. 앱이 삭제되거나 마이그레이션된 후에도 PVC가 남아 스토리지를 소비하고 비용을 증가시킵니다.

쿠버네티스 v1.37에서는 PVC "마지막 사용" 추적이 `PersistentVolumeClaimUnusedSinceTime` 기능 게이트 뒤에서 베타로 승격됩니다. 이 기능은 알파(v1.36)에서는 기본적으로 비활성화되어 출시되었지만 이제 기본적으로 활성화됩니다. 기존 PVC 보호 컨트롤러가 관리하는 새로운 `Unused` 컨디션이 `PersistentVolumeClaimStatus`에 추가됩니다. PVC를 참조하는 마지막 비종료 파드가 사라지면 `Status=True (Reason=NoPodsUsingPVC)`가 되고, 파드가 다시 참조하기 시작하는 즉시 `Status=False (Reason=PodUsingPVC)`가 됩니다. 컨디션의 `lastTransitionTime`은 "미사용 시작" 타임스탬프 역할도 하므로, 쿠버네티스가 마지막으로 PVC를 사용한 파드를 추적하거나 자체적으로 삭제 결정을 내리지 않아도 관리자가 PVC의 실제 유휴 기간을 조회할 수 있습니다. 삭제 결정은 전적으로 관리자에게 맡깁니다. 타임스탬프는 인프라 수준에서 볼륨이 마운트 해제된 정확한 시점이 아니라 컨트롤러가 PVC를 사용하는 파드가 없다고 관찰한 시점을 반영하므로, 보고된 유휴 시간이 실제보다 약간 짧을 수는 있지만 더 길게 표시되지는 않는다는 점에 유의해야 합니다.

이 작업은 [SIG Storage](https://www.kubernetes.dev/community/community-groups/sigs/storage/)가 주도한 [KEP #5541](https://www.kubernetes.dev/resources/keps/5541/)의 일환으로 진행되었습니다.

### etcd RangeStream 지원

`etcd`의 단항 `Range` RPC는 응답 전체를 메모리에 만든 뒤 전송하므로 규모가 커지면 문제가 됩니다. 큰 목록을 처리할 때, 예를 들어 대규모 클러스터에서 kube-apiserver의 watch 캐시를 준비할 때 원시 키-값 슬라이스, 직렬화된 protobuf 형식, gRPC 전송 버퍼가 모두 한꺼번에 메모리에 존재해야 하며, 그로 인한 메모리 사용량 급증은 kube-apiserver에도 영향을 줍니다. 페이지네이션도 근본적인 비용을 해결하지 못합니다. 페이지마다 전체 결과 수를 다시 계산하기 위해 B-트리 인덱스 전체를 계속 순회하므로, 페이지마다 `O(limit)`이어야 할 연산이 `O(total_keys)`가 됩니다.

쿠버네티스 v1.37은 `EtcdRangeStream` 기능 게이트(`kube-apiserver` 전용, 기본적으로 **활성화**) 뒤에서 `etcd` `RangeStream` 지원을 바로 베타로 출시합니다.
이번 릴리스는 기존 `RangeRequest`를 재사용하되 버퍼링된 하나의 큰 데이터 대신 청크를 반환하는 새로운 서버 스트리밍 `RangeStream` RPC를 추가합니다. 서버는 적응형 청크 크기 조절 방식으로 내부 페이지네이션을 수행하고, 각 청크의 목표 크기는 `MaxRequestBytes`와 지금까지 관찰된 값 크기를 기준으로 조정됩니다. 단일 MVCC 리비전을 고정하여 병합된 스트림의 스냅샷 일관성을 유지하고, 별도 인덱스 순회 대신 스트리밍 중 누적한 실행 집계에서 전체 키 수를 구합니다.
주요 사용자는 `kube-apiserver`의 watch 캐시 초기화이며, 이제 전체 목록을 먼저 메모리에 조립하지 않고 각 청크가 도착하는 즉시 인라인에서 가상의 _created_ 이벤트로 디코딩합니다. `WatchList`가 비활성화된 경우 직접 `GetList`를 호출할 때도 동일하게 처리합니다.

이 기능을 사용하려면 `etcd` 3.7 이상이 필요합니다. 이전 버전의 `etcd`를 사용하면 `kube-apiserver`가 Unimplemented 응답을 감지하고 동작 변경 없이 단항 `Range`로 자동 폴백합니다. 고정한 리비전이 스트리밍 도중 압축되면 `kube-apiserver`는 다른 watch 캐시 초기화 실패와 동일하게 처리하고 재시도합니다. 이는 페이지네이션된 List 호출에서 이미 발생할 수 있는 압축 경쟁보다 나쁘지 않습니다. 베타 승격 기준에는 5,000노드 클러스터에서 대규모 목록 지연 시간을 측정하는 확장성 테스트가 포함되며, 새 RPC를 직접 시험하려는 사용자를 위해 `etcdctl get --stream`도 함께 제공됩니다.

이 작업은 [SIG etcd](https://www.kubernetes.dev/community/community-groups/sigs/etcd/)가 주도한 [KEP #5966](https://www.kubernetes.dev/resources/keps/5966/)의 일환으로 진행되었습니다.

### 동시 watch 오브젝트 디코딩

`kube-apiserver`는 단일 고루틴에서 `etcd`의 모든 watch 이벤트를 한 번에 하나씩 디코딩하고 변환합니다. 따라서 이벤트별 변환 하나가 느리면, 특히 CRD 변환 웹훅 호출이 느리면 뒤에 대기 중인 모든 이벤트가 차단됩니다. 내장 리소스에서는 대부분 불편한 정도지만, 제공 버전과 저장 버전이 다른 CRD의 콜드 캐시를 직렬로 변환하면 몇 분이 걸릴 수 있습니다. 이 시간이 `etcd`의 기본 5분 압축 주기를 초과하면 캐시가 읽기 시작한 리비전이 초기화 완료 전에 압축되어 watch를 재개할 수 없고, 초기화가 계속 다시 시작되어 리소스가 충분히 크면 끝내 수렴하지 못합니다. 그동안 해당 리소스의 목록 조회나 watch를 시도하는 모든 클라이언트에는 오류가 발생합니다.

`ConcurrentWatchObjectDecode` 게이트는 사실 v1.31부터 베타였고 기본적으로 비활성화되어 있었지만, 쿠버네티스 v1.37에서 기본 활성화로 전환됩니다. 이 기능을 활성화하면 단일 고루틴 대신 제한된 워커 고루틴 풀(기본값 10개이며, 8~12개 부근부터 효과가 둔화된다는 실험 결과를 반영해 조정)에서 디코딩 및 변환 단계를 수행합니다. 수집기는 전달 전에 이벤트를 원래 순서로 다시 조립하므로 이벤트 순서가 정확히 유지됩니다. 15만 개 파드를 사용한 벤치마크에서 동시 디코딩만으로 캐시 초기화 시간이 약 40% 줄었고, 이번 릴리스에 함께 도입되는 새로운 `EtcdRangeStream` 기능(KEP 5966 참고)과 결합하면 약 55% 줄었습니다. 주의할 주요 절충점은 변환 웹훅 부하입니다. 이 기능을 활성화하면 캐시 초기화 중 한 번에 하나씩 실행되던 변환이 웹훅에 대해 최대 10개까지 동시에 실행될 수 있습니다. 전체 호출량은 같고 동시 실행 수만 달라지므로, 자체 동시 실행 수를 10 미만으로 제한하는 웹훅에 주로 영향을 줍니다.

이 작업은 [SIG API Machinery](https://www.kubernetes.dev/community/community-groups/sigs/api-machinery/)가 주도한 [KEP #6178](https://www.kubernetes.dev/resources/keps/6178/)의 일환으로 진행되었습니다.

### 오래된 컨트롤러 완화 {#stale-controller-mitigation}

`kube-controller-manager`의 모든 컨트롤러는 `kube-apiserver`를 watch하여 만든 로컬 캐시를 사용하며, 이 watch
스트림은 최종적 일관성만 보장합니다. 변경 사항이 밀리초 내에 나타날 수도 있고 부하가 크면 몇 초 또는 몇 분이
걸릴 수도 있습니다. 현재 운영자는 이러한 지연을 확인할 수 없고 정상적인 지연과 위험할 정도로 동기화가 뒤처진 컨트롤러를
구분할 방법도 없습니다. 따라서 컨트롤러가 이미 오래된 상태를 기준으로 계속 조정할 수 있습니다.

오래된 컨트롤러 완화 기능은 v1.36부터 컨트롤러별 `StaleControllerConsistency<Controller>`
기능 게이트 뒤에서 기본 활성화된 베타 기능입니다. 쿠버네티스 v1.37에서는 이를 HorizontalPodAutoscaler 컨트롤러로 확장하고 아래 설명된 회로 차단 변형과
추가 메트릭을 더합니다. 핵심 메커니즘은
_자신이 쓴 값 읽기(read your writes)_ 보장입니다. client-go의 `ResourceEventHandlerFuncs`에 새 `BookmarkFunc` 콜백을 추가하여 컨트롤러가
기존 add/update/delete 콜백이 놓치는 예외 상황에서도 관련 오브젝트의 리소스 버전을 안정적으로 추적할 수 있게 합니다. 컨트롤러는
자신이 작성한 값의 리소스 버전을 기록하고 다음 조정 시 인포머 캐시가 실제로 해당 쓰기 작업을 따라잡을 때까지
건너뛰고 다시 큐에 넣습니다. 데몬셋(DaemonSet) 컨트롤러가 좋은 예입니다. 이 컨트롤러는
DaemonSet → Pod 리소스 버전을 추적하여 오래된 파드 캐시를 기준으로 다시 조정하지 않습니다. 두 번째 회로 차단
변형은 node-lifecycle처럼 지연 시간에 민감한 컨트롤러를 대상으로 합니다. 이런 컨트롤러는 캐시에서 오래된 노드 리스를 읽고
만료되었다고 잘못 판단할 수 있습니다. 대신 중단을 일으키는 결정을 내릴 때 라이브 GET을 수행하고 캐시가 따라잡을 때까지
오래된 읽기를 기준으로 동작하지 않고 캐시를 "준비되지 않음"으로 표시합니다. `StaleControllerConsistency`는 완화 기능 자체를 제어하며,
처음에는 KCM이 대규모로 표시한 컨트롤러로 범위를 제한합니다. `MonitorInformerStaleness`는 별도의 관찰 전용 게이트로,
인포머 캐시가 실제로 얼마나 뒤처졌는지 보여주기 위해서만 5초마다 API 서버를 직접
폴링합니다. `AtomicFIFO`와 `UnlockWhileProcessingFIFO`는 이 완화 기능이 의존하는 client-go 워크큐 기반 요소입니다. 이 중 어느 것도
기본 조정자 동작을 바꾸지 않습니다. 일시 중지되어 다시 큐에 들어간 컨트롤러는 실제로 캐시를 기다리는 중인데도 멈춘 것처럼 보일 수 있으며,
되돌릴 수 없는 작업을 수행하지 않으므로 깔끔하게 롤백됩니다.

이 작업은 [SIG API Machinery](https://www.kubernetes.dev/community/community-groups/sigs/api-machinery/)가 주도한 [KEP #5647](https://www.kubernetes.dev/resources/keps/5647)의 일환으로 진행되었습니다.

### 매니페스트 기반 어드미션 제어 구성

쿠버네티스에서 어드미션 제어는 리소스가 API에 수락되기 전에 정책을 적용하는 역할을
합니다. 하지만 쿠버네티스 API를 통해 구성된 어드미션 웹훅과 정책은 클러스터 시작 시 API 서버와
etcd에 의존하며, 어드미션 구성 리소스 자체를 보호할 수 없습니다. 이로 인해 클러스터
부트스트랩 중에 공백이 생기고 충분한 특권 접근 권한이 있는 사용자가 중요한 어드미션 정책을 변경하거나 제거할 수 있습니다.

쿠버네티스 v1.37에서 [매니페스트 기반 어드미션 제어](/docs/reference/access-authn-authz/manifest-admission-control/) 구성이 베타로 승격되어, 어드미션 웹훅과 CEL 기반

정책을 디스크의 매니페스트 파일에서 불러와 API 서버 시작 시점부터 적용할 수 있습니다. 구성은 쿠버네티스 API와
독립적으로 관리되므로 API 기반 어드미션 리소스의 변경도 막을 수 있습니다. 매니페스트 파일의
변경 사항을 감시하여 유효한 업데이트는 자동으로 다시 불러오고, 유효하지 않은 업데이트가 있으면 이전에 불러온
구성을 그대로 유지합니다.

이 작업은 [SIG API Machinery](https://www.kubernetes.dev/community/community-groups/sigs/api-machinery/)가 주도한 [KEP #5793](https://www.kubernetes.dev/resources/keps/5793/)의 일환으로 진행되었습니다.


### 복호화할 수 없는 리소스 처리 개선

쿠버네티스는 리소스를 etcd에 저장하며, 저장 데이터 암호화를 사용해 민감한 데이터를 보호할 수 있습니다. 하지만 암호화된
리소스를 더 이상 복호화할 수 없으면, 예를 들어 암호화 키를 사용할 수 없으면 API 서버가 해당 리소스를 정상적으로 읽거나
관리할 수 없습니다. 이로 인해 쿠버네티스 API를 통해 접근할 수 없는 리소스가 클러스터에 남을 수 있으며,
관리자가 이를 복구하려면 기반 etcd 데이터를 수동으로 수정해야 합니다.

쿠버네티스 v1.37은 클러스터 관리자가 API 서버에서 복호화할 수 없는 리소스를 식별하고 제거할 수 있도록 베타 지원을 제공합니다.

이 기능은 이전에는 알파였고 쿠버네티스 v1.32에서 도입되었으며, 문제가 있는 API 리소스를 직접

etcd 파일을 조작하지 않고 쿠버네티스 API를 통해 제거할 수 있게 합니다. 또한 관리자가 삭제 전에
영향을 받는 리소스를 검증할 수 있는 보호 장치를 제공합니다.

이 작업은 [SIG Auth](https://www.kubernetes.dev/community/community-groups/sigs/auth/)가 주도한 [KEP #3926](https://www.kubernetes.dev/resources/keps/3926/)의 일환으로 진행되었습니다.

## 새로운 알파 기능

### 스테이트풀셋 롤아웃을 위한 새로운 `Recreate` 전략

쿠버네티스 v1.37은 스테이트풀셋(StatefulSet) 롤아웃을 위한 `Recreate` 전략을 도입합니다. StatefulSet API는 이전에 두 가지 업데이트
전략, 즉 OnDelete(수동)와 RollingUpdate(자동, 기본값)만 제공했습니다. 디플로이먼트(Deployment)와 마찬가지로 `Recreate` 업데이트 전략은 스테이트풀셋의
`.spec.template` 변경 사항을 반영하는 새 파드를 만들기 전에 StatefulSet의 모든 파드를
삭제합니다. 이 전략을 사용하려면 `StatefulSetRecreateStrategy` [기능 게이트](/docs/reference/command-line-tools-reference/feature-gates/#StatefulSetRecreateStrategy)를 활성화해야 합니다.

이 작업은 [SIG Apps](https://www.kubernetes.dev/community/community-groups/sigs/apps/)가 주도한 [KEP #3541](https://www.kubernetes.dev/resources/keps/3541/)의 일환으로 진행되었습니다.

### 주목할 DRA 알파 기능

#### DRA: 노드 할당 가능 리소스 요청

쿠버네티스 v1.37은 CPU, 메모리, huge page 같은 노드 리소스를 DRA로 관리하는 알파 지원을 개선합니다.
표준 리소스 계산과 DRA 리소스 계산을 통합하여 같은 노드 용량이 두 번 계산되지 않도록 합니다.

이번 업데이트는 `mapping`(CPU/메모리 DRA 드라이버처럼 코어 리소스를 직접 모델링하는 장치용)과 `overhead`(가속기 장치를 위한 보조 호스트 메모리 등)를 위한 별도의 API 필드를 도입합니다. 이제 kubelet은 파드 및 컨테이너 cgroup 전체에 이러한 할당을 적용하고, 이를 메모리 QoS, OOM 점수 계산, 인플레이스 파드 리사이즈와 통합합니다.

이 작업은 [KEP #5517](https://www.kubernetes.dev/resources/keps/5517/)의 일환으로 진행되었으며,
[SIG Scheduling](https://www.kubernetes.dev/community/community-groups/sigs/scheduling/)이 [SIG Node](https://www.kubernetes.dev/community/community-groups/sigs/node/)의 참여를 받아 주도했습니다.

#### DRA: 파생 속성

쿠버네티스 v1.37은 [DRA의 파생 속성](/docs/concepts/resource-management/dynamic-resource-allocation/dra-api/#derived-attributes)에 대한 알파 지원을 도입합니다. 워크로드는 CEL 표현식을 사용해 장치 정보에서 가상
속성을 만들고 관련 장치를 선택할 때 사용할 수 있습니다.

이를 통해 GPU와 네트워크 인터페이스 같은 장치를 드라이버에서 서로 다른
속성 이름이나 형식을 사용하더라도 더 쉽게 함께 배치할 수 있습니다. 예를 들어 워크로드는 공용 NUMA 식별자를 파생하고 이를 사용해
토폴로지가 일치하는 장치를 선택할 수 있습니다.

이 작업은 [SIG Scheduling](https://www.kubernetes.dev/community/community-groups/sigs/scheduling/)이 [SIG Network](https://www.kubernetes.dev/community/community-groups/sigs/network/)의 참여를 받아 주도한 [KEP #6080](https://www.kubernetes.dev/resources/keps/6080/)의 일환으로 진행되었습니다.

#### DRA: 장치 호환성 그룹 {#dra-device-compatibility-groups}

DRA는 서로 다른 파티셔닝 또는 가상화 방식을 지원하는 장치를 관리하는 데 사용할 수 있습니다. 하지만 GPU의 MIG와 vGPU처럼
일부 구성은 동일한 물리 장치에서 함께 사용할 수 없습니다. 이전에는 이러한
비호환성을 스케줄러가 이미 결정을 내린 후 장치 준비 과정에서만 감지할 수 있었습니다.

쿠버네티스 v1.37에서 DRA는 장치 호환성 그룹을 추가하여 리소스 드라이버가 함께
할당할 수 있는 장치를 설명할 수 있게 합니다. 스케줄러는 할당 결정을 내릴 때 이 정보를 사용해 호환되지 않는 장치가
함께 할당되는 것을 막고, 호환되지 않는 장치 구성으로 인한 파드 시작 실패를 방지할 수 있습니다.

이 작업은 [SIG Scheduling](https://www.kubernetes.dev/community/community-groups/sigs/scheduling/)이 주도한 [KEP #5963](https://www.kubernetes.dev/resources/keps/5963/)의 일환으로 진행되었습니다.

### 인플레이스 파드 리사이즈를 위한 스케줄러 선점 {#scheduler-preemption-in-place-pod-resize}

쿠버네티스 v1.37은 선택적으로 활성화하는 알파 `InPlacePodVerticalScalingSchedulerPreemption` 기능 게이트 뒤에서 _인플레이스 파드 리사이즈를 위한 스케줄러 선점_을 도입합니다. 이 변경은 핵심 [인플레이스 파드 수직 스케일링](/docs/concepts/workloads/pods/pod-lifecycle/#pod-resize-inplace) 기능이 스테이블로 승격된 뒤에도 남아 있던 중요한 기능 공백을 해결합니다. 실행 중인 파드가 노드의 사용 가능한 용량을 초과하는 추가 리소스를 요청하면 `kubelet`이
요청을 `Deferred`로 표시하여 노드에 충분한 리소스가 생길 때까지 파드를 기다리게 했습니다. 이
개선 사항을 통해 쿠버네티스 컨트롤 플레인은 사용률이 100%인 노드에서 용량을 능동적으로 확보하고 우선순위가 낮은
워크로드를 선점하여, 대기 중인 중요 고우선순위 애플리케이션의 인플레이스 리사이즈 요청을 성공시킬 수 있습니다.

이 작업은 [SIG Scheduling](https://www.kubernetes.dev/community/community-groups/sigs/scheduling/)이 주도한 [KEP #5836](https://www.kubernetes.dev/resources/keps/5836/)의 일환으로 진행되었습니다.

### 메모리 기반 볼륨의 동적 리사이즈

인플레이스 파드 수직 스케일링을 기반으로 하는 알파 _메모리 기반 볼륨의 인플레이스 스케일링_ 기능은 파드의

`/resize` 하위 리소스를 확장합니다. 이 하위 리소스는 이전에는 컨테이너를 다시 시작하지 않고 동적으로 CPU와 메모리를 조정하는 기능만 제공했지만,
이제 실행 중인 파드에서 메모리 기반(medium: Memory) `emptyDir` 볼륨의 `sizeLimit` 업데이트도 지원합니다. 볼륨의 `sizeLimit`을
/resize 하위 리소스를 통해 명시적으로 조정하면, Kubelet은 컨테이너를 중단하지 않고 기반 tmpfs 마운트를 동적으로 업데이트하는 동시에
메모리 부족 오류나 오탐 축출 트리거를 안전하게 방지합니다. 이 기능은 인메모리 임시 스토리지에 의존하는
스테이트풀 및 메모리 집약형 워크로드에 특히 유용하며, 파드 재시작이나 애플리케이션 중단 없이 컨테이너 메모리 용량과 함께 스토리지
한도를 동적으로 확장할 수 있습니다.


이 기능은 옵트인 방식의 기본 비활성 알파 기능입니다. 사용하려면

`InPlacePodVerticalScalingMemoryBackedVolumes` 기능 게이트를 활성화합니다.

이 작업은 [SIG Node](https://www.kubernetes.dev/community/community-groups/sigs/node/)와 [SIG Storage](https://www.kubernetes.dev/community/community-groups/sigs/storage/)가 주도한 [KEP #6030](https://www.kubernetes.dev/resources/keps/6030/)의 일환으로 진행되었습니다.

### 노드의 특수 라이프사이클 관리

여러 쿠버네티스 컴포넌트가 노드의 라이프사이클 상태를 파악해야 하지만, 현재는 각 컴포넌트가 서로 다른 조합의
노드 준비성, 테인트, 파드 상태, 레이블, 어노테이션, 제공자 API를 기준으로 이를 추론합니다. 이 개선 사항은 노드에 잘 알려진
라이프사이클 컨디션을 도입하여 관리자가 코어
컨트롤러와 생태계 도구에서 사용할 수 있는 라이프사이클 상태를 게시하는, 쿠버네티스가 소유한 단일 위치를 제공합니다. 새로운 노드 컨디션은 `DrainInProgress`, `Drained`, `MaintenancePlanned`, `MaintenanceInProgress`, `GracefulNodeShutdownInProgress`입니다.

이 작업은 [SIG Node](https://www.kubernetes.dev/community/community-groups/sigs/node/)가 주도한 [KEP #5683](https://www.kubernetes.dev/resources/keps/5683/)의 일환으로 진행되었습니다.

### WAS: 주목할 알파 기능

#### CompositePodGroup API

이전 릴리스에서는 평면 구조의 워크로드에 대한 갱 스케줄링 지원을
도입했지만, 현대의 AI/ML 워크로드는 복잡하고 더 정교한
스케줄링 요구 사항이 있습니다. 쿠버네티스 v1.37의 새로운 알파 `CompositePodGroup`
API를 사용하면 쿠버네티스가 복잡한 워크로드를 평면적인 파드 집합 대신
그룹의 계층 구조로 설명할 수 있습니다. 이를 통해 다단계 갱 스케줄링,
워크로드 인지 선점, 토폴로지 인지 스케줄링을 사용할 수 있습니다.

이 작업은 [SIG Scheduling](https://www.kubernetes.dev/community/community-groups/sigs/scheduling/)이 주도한 [KEP #6012](https://www.kubernetes.dev/resources/keps/6012/)의 일환으로 진행되었습니다.

#### 워크로드 인지 스케줄링 컨트롤러 API

쿠버네티스 v1.37은 알파 기능으로 워크로드 컨트롤러(JobSet, TrainJob, LWS, RayJob과 `Job` 같은 코어 워크로드)를 _워크로드 인지 스케줄링(Workload-aware Scheduling)_(WAS)과 통합하는 공통 프레임워크를 제공합니다.
쿠버네티스 v1.37은 알파 기능으로 워크로드 컨트롤러(JobSet, TrainJob, LWS, RayJob과 `Job` 같은 코어 워크로드)를 _워크로드 인지 스케줄링(Workload-aware Scheduling)_(WAS)과 통합하는 공통 프레임워크를 제공합니다.

이 프레임워크는 _토폴로지 제약 조건_과 _중단 정책_ 같은 재사용 가능한 `scheduling.k8s.io` API 기본 요소와
스케줄링 리소스 생성을 처리하는 공유 라이브러리를 제공합니다. 이를 통해 컨트롤러는 동일한 스케줄링 로직을 별도로 구현하지 않고도
자체 API에서 일관된 방식으로 WAS 기능을 네이티브하게 노출할 수 있습니다.

이 작업은 [SIG Scheduling](https://www.kubernetes.dev/community/community-groups/sigs/scheduling/)이 주도한 [KEP #6089](https://www.kubernetes.dev/resources/keps/6089/)의 일환으로 진행되었습니다.

#### 워크로드 API와 잡 컨트롤러 통합 {#workload-apis-job-controller}

이 기능은 쿠버네티스 v1.36에서 제한된 기능으로 처음 도입되었으며, [워크로드 인지 스케줄링 컨트롤러 API](#워크로드-인지-스케줄링-컨트롤러-api)를 기반으로 쿠버네티스 v1.37의 `batch/v1` Job에 새로운 사용자용 `spec.scheduling` 필드를 추가하여 사용자가
스케줄링 정책, 토폴로지 제약 조건, 중단 모드, 리소스 클레임을 명시적으로 구성할 수 있게 합니다.
`spec.scheduling`을 생략하면 Job은 기본 스케줄링을 사용하여 기존 동작을 유지하는 동시에 minCount 게이트를 적용하지 않는
워크로드 인지 스케줄링용 기본 Workload/PodGroup을 생성합니다. 사용자는 명시적으로 갱
스케줄링을 사용하도록 선택할 수 있습니다. 이때 `minCount`는 기본적으로 Job의 병렬 처리 수가 되며, 컨트롤러는 공유 `workloadbuilder` 라이브러리를 사용해
사용자 정의 변환 로직을 구현하는 대신 스케줄링 구성을 해당 Workload 및 PodGroup 오브젝트로
변환합니다.

이 작업은 [SIG Scheduling](https://www.kubernetes.dev/community/community-groups/sigs/scheduling/)이 주도한 [KEP #5547](https://www.kubernetes.dev/resources/keps/5547/)의 일환으로 진행되었습니다.

### `nftables`용 localhost NodePort 유저스페이스 프록시

쿠버네티스 v1.37은 `nftables` `kube-proxy` 백엔드에 선택적으로 활성화하는 유저스페이스 프록시를 추가하여 IPv4와 IPv6에서
`localhost`를 통해 NodePort 서비스에 접근할 수 있게 합니다. `nftables`가 이전에는 localhost NodePort를
제공할 수 없었던 `nftables`와 `iptables` 백엔드 간의 격차를 해소합니다.

`kube-proxy` `--nodeport-addresses` 구성에 `localhost` 또는 루프백 주소가 포함되면
프록시가 활성화됩니다. 이는 `localhost:<NodePort>` 연결에 의존하는 로컬 컨테이너 레지스트리 같은
워크로드에 유용할 수 있습니다. `iptables`와 `ipvs` 백엔드의 기존 동작은 변경되지 않습니다.

이 작업은 [SIG Network](https://www.kubernetes.dev/community/community-groups/sigs/network/)가 주도한 [KEP #6032](https://www.kubernetes.dev/resources/keps/6032/)의 일환으로 진행되었습니다.

## 그 밖의 주요 변경 사항

### 스테이트풀셋의 `maxUnavailable`이 다시 기본 활성화

스테이트풀셋의 `maxUnavailable` 필드는 v1.36에서 버그가 발견된 뒤 쿠버네티스 v1.37에서 다시 기본적으로
활성화되었습니다.

초기 StatefulSet 리비전에 결함이 있어 준비 상태가 되지 않는 파드가 생성되고
`MaxUnavailableStatefulSet`이 활성화된 상태에서 StatefulSet 컨트롤러가 해당 파드를 수정된 새
리비전으로 업데이트하지 못하는 버그였습니다. 버그가 발생하면 영향을 받은 파드가 CrashLoopBackOff 상태에 무기한 머물 수 있었습니다([kubernetes#137409](https://github.com/kubernetes/kubernetes/issues/137409) 참고).


### `nftables` 성능 개선

이제 kube-proxy는 `nft` 커맨드라인 도구를 거치지 않고 커널의 netlink 인터페이스로 nftables 규칙을 처리합니다. 이에 따라 kube-proxy가 nftables 규칙을 더 효율적으로 검사하고 관리하여 규칙 관리 성능이 향상됩니다.

### client-go의 컨텍스트 처리 및 컨텍스트 로깅

client-go의 컨텍스트 전파 및 컨텍스트 로깅 지원이 완료되었습니다. 다만 기반 API가 컨텍스트
전달을 지원하지 않아 전역 klog 로거에 계속 의존하는 소수의 인증 플러그인 로그 호출은
예외입니다.

## v1.37의 승격, 사용 중단, 제거 사항

### 스테이블로 승격

여기에는 스테이블(일반적으로 사용 가능이라고도 함)로 승격된 모든 기능을 나열합니다. 알파에서 베타로 승격된 기능과 신규 기능을 포함한
전체 업데이트 목록은 릴리스 노트를 참고합니다.

이번 릴리스에서 총 16개의 개선 사항이 스테이블로 승격되었습니다.

* [재귀적 SELinux 레이블 변경 속도 향상](https://www.kubernetes.dev/resources/keps/1710/)
* [ClusterTrustBundles](https://www.kubernetes.dev/resources/keps/3257/)
* [파드 인증서](https://www.kubernetes.dev/resources/keps/4317/)
* [파드 호스트네임에 임의의 FQDN 설정 허용](https://www.kubernetes.dev/resources/keps/4762/)
* [DRA: 표준화할 수 있는 네트워크 인터페이스 데이터를 포함한 ResourceClaim 상태](https://www.kubernetes.dev/resources/keps/4817/)
* [HorizontalPodAutoscaler의 구성 가능한 허용 오차](https://www.kubernetes.dev/resources/keps/4951/)
* [완화된 서비스 이름 검증](https://www.kubernetes.dev/resources/keps/5311/)
* [장치 플러그인 및 DRA를 위한 파드 상태에 리소스 상태 추가](https://www.kubernetes.dev/resources/keps/4680/)
* [DRA: 장치 테인트와 톨러레이션](https://www.kubernetes.dev/resources/keps/5055/)
* [DRA: DRA 드라이버를 통한 확장 리소스 요청 처리](https://www.kubernetes.dev/resources/keps/5004/)
* [노드 선언 기능](https://www.kubernetes.dev/resources/keps/5328/)
* [샌드박스 생성을 위한 컨디션 추가](https://www.kubernetes.dev/resources/keps/3085/)
* [스토리지 버전 마이그레이터를 트리 내부로 이동](https://www.kubernetes.dev/resources/keps/4192/)
* [견고한 watch 캐시 초기화](https://www.kubernetes.dev/resources/keps/4568/)
* [DRA: 표준 numaNode 장치 속성](https://www.kubernetes.dev/resources/keps/6072/)
* [metrics.k8s.io API 정의](https://www.kubernetes.dev/resources/keps/5207/)
* [KYAML](https://www.kubernetes.dev/resources/keps/5295/)

## 사용 중단, 제거, 커뮤니티 업데이트

쿠버네티스가 발전하고 성숙함에 따라 프로젝트의 전반적인
건전성을 위해 기능을 사용 중단하거나 제거하거나 더 나은 기능으로 대체할 수 있습니다.
이 과정에 대한 자세한 내용은 쿠버네티스 [사용 중단 및 제거 정책](/docs/reference/using-api/deprecation-policy/)을 참고합니다.
이러한 사용 중단 및 제거 사항 중 다수는 [사용 중단 및 제거 블로그](/blog/2026/07/31/kubernetes-v1-37-sneak-peek/)에서 발표되었습니다.

### `kube-dns` 사용 중단

CoreDNS는 쿠버네티스 v1.13부터 기본 클러스터 DNS 애드온이었으며, `kube-dns`는 그 이후 발전을 따라가지 못했습니다. EndpointSlice 및 듀얼 스택 서비스 같은 기능은 여기에서 사용할 수 없습니다.

쿠버네티스는 이미 kube-dns 서브프로젝트를 종료했으며, node-local-dns는 자체 [리포지터리](https://github.com/kubernetes-sigs/node-local-dns)로 분리되어 계속 유지 관리되고 CoreDNS와 함께 작동합니다. v1.40 이후에는 kube-dns용 새 패키지를 더 이상 빌드하지 않을 것으로 예상됩니다.

여전히 `kube-dns`를 실행한다면 [클러스터를 CoreDNS로 마이그레이션할 계획을 세우기 시작합니다](/docs/tasks/administer-cluster/coredns/).

### `kube-proxy`의 `ipvs` 모드 지원 사용 중단

`kube-proxy`의 `ipvs` 모드 지원은 `iptables` 성능 병목 현상을 해결하기 위해 v1.8에서 도입되었습니다. 하지만
커널 `ipvs` API만으로는 쿠버네티스 서비스를 완전히 구현할 수 없으므로 `ipvs` 모드는 기반에서 계속 `iptables`를 사용합니다.
([KEP-3866, "kube-proxy의 ipvs 모드는 우리를 구하지 못한다"](https://github.com/kubernetes/enhancements/blob/master/keps/sig-network/3866-nftables-proxy/README.md#the-ipvs-mode-of-kube-proxy-will-not-save-us)).

이제 `ipvs` 모드에서 `kube-proxy`를 실행하는 클러스터(또는 KubeProxyConfiguration에서 mode가 `ipvs`인 경우)는 시작 시 사용 중단 경고를 기록합니다. 사용 중단 일정은 다음과 같습니다.
- v1.40까지 `kube-proxy`의 `ipvs` 모드는 기본적으로 비활성화될 예정입니다(기능 게이트를 통해 계속 선택 가능).
- v1.43까지 `ipvs` 모드 지원이 완전히 제거될 예정입니다([KEP #5495 승격 기준](https://github.com/kubernetes/enhancements/blob/master/keps/sig-network/5495-deprecate-ipvs-mode-in-kube-proxy/README.md#graduation-criteria)).
현재 실행 중인 모드를 확인하려면 다음을 사용합니다.

```bash
kubectl -n kube-system get configmap kube-proxy -o jsonpath='{.data.config\.conf}' | grep 'mode:'
```

이 사용 중단의 근거를 이해하려면 [KEP #5495](https://www.kubernetes.dev/resources/keps/5495/)를 참고합니다.

### `kubectl`: `kubectl run --filename/-f` 사용 중단 예정

생성된 파드는 항상 `NAME`, `--image` 같은 CLI 인자만으로 빌드되므로 `kubectl run`의 `--filename`(또는 `-f`) 플래그는 사용 중단될 예정입니다.

원본 이슈와 논의는 [kubernetes/kubernetes#138671](https://github.com/kubernetes/kubernetes/issues/138671)을 참고합니다.

### `kubelet`: 스태틱 파드에서 더 이상 시크릿 또는 컨피그맵 참조 불가

스태틱 파드는 API 서버를 통해 생성되지 않으므로 API 리소스를 직접 읽도록 설계되지 않았지만, 버그로 인해 `configMapRef` 또는 `secretRef` 같은 필드를 통해 시크릿(Secret)이나 컨피그맵(ConfigMap)을 참조할 수 있었습니다. 이제 이 버그가 수정되었습니다. v1.37부터 이러한 참조는 엄격히 금지되며, 이전에 이 제한을 사용하지 않도록 선택할 수 있게 했던 `PreventStaticPodAPIReferences` 기능 게이트는 제거되었습니다.

원본 이슈와 논의는 [kubernetes/kubernetes#140226](https://github.com/kubernetes/kubernetes/issues/140226)을 참고합니다.

### 진행 중인 주요 변경 사항: 향후 cgroup v1 지원 제거

현대적인 리눅스 배포판과 컨테이너 런타임은 [cgroup v2](/docs/concepts/architecture/cgroups/)를 기본값으로 사용하므로,
레거시 cgroup v1 지원을 공식적으로 단계적 폐지하고 있습니다. v1.35 릴리스부터 `failCgroupV1` 설정의
기본값은 true입니다. 따라서 명시적 구성 재정의를 적용하지 않으면 cgroup v1에 계속 의존하는 모든 노드에서
`kubelet` 초기화가 실패합니다.

```yaml
apiVersion: kubelet.config.k8s.io/v1beta1
kind: KubeletConfiguration
failCgroupV1: false # 임시 재정의
```

이 재정의는 단기적인 해결책으로만 간주해야 합니다. 메모리 QoS와 메모리 기반 볼륨의 인플레이스 스케일링 같은 고급 리소스 관리 기능은 cgroups v2에서만 작동합니다. 쿠버네티스
v1.37에서도 재정의를 계속 사용할 수 있지만, 향후 릴리스에서 cgroups v1 지원을 제거할 예정이므로 cgroups v2로 마이그레이션하는 것이 좋습니다.

이 사용 중단에 대해 자세히 알아보려면 [KEP #5573](https://www.kubernetes.dev/resources/keps/5573/)을 참고합니다.

### 릴리스 노트

쿠버네티스 v1.37 릴리스의 전체 세부 사항은 [릴리스 노트](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.37.md)에서 확인합니다.

### 다운로드 및 시작하기

[쿠버네티스 v1.37](/releases/1.37/)은
[쿠버네티스 다운로드 페이지](/releases/download/) 또는 [GitHub](https://github.com/kubernetes/kubernetes/releases/tag/v1.37.0)에서 직접 다운로드할 수 있습니다.

쿠버네티스를 시작하려면 [튜토리얼](/docs/tutorials/)을 확인하거나 [minikube](https://minikube.sigs.k8s.io/)로 로컬 쿠버네티스 클러스터를 실행합니다.
[kubeadm](/docs/setup/independent/create-cluster-kubeadm/)으로도 v1.37을 쉽게 설치할 수 있습니다.

### 릴리스 팀

쿠버네티스는 커뮤니티의 지원, 헌신, 노력으로만 존재할 수 있습니다.
각 릴리스 팀은 사용자가 의지하는 쿠버네티스 릴리스를 이루는 수많은 요소를 함께 만드는
헌신적인 커뮤니티 자원봉사자로 구성됩니다.

이를 위해서는 코드 자체부터 문서화와 프로젝트 관리까지 커뮤니티 곳곳에 있는 사람들의 전문
기술이 필요합니다.

쿠버네티스 v1.37 릴리스를 커뮤니티에 제공하기 위해 오랜 시간 열심히 작업한 전체 [릴리스 팀](https://github.com/kubernetes/sig-release/blob/master/releases/release-1.37/release-team.md)에 감사드립니다.

릴리스 팀에는 처음 참여하는 섀도부터 여러 릴리스 주기를 거쳐 경험을 쌓고 다시 참여한 팀 리드까지
다양한 구성원이 있습니다.

성공적인 릴리스 주기 내내 우리를 지원하고 옹호하며 모두가 최선의 방식으로 기여할 수 있도록 하고
릴리스 프로세스를 개선하도록 독려해 준 릴리스 리드 [Dipesh Rawat](https://github.com/dipesh-rawat)에게
특별히 깊은 감사를 전합니다.

### 프로젝트 속도

CNCF K8s [DevStats](https://k8s.devstats.cncf.io/d/11/companies-contributing-in-repository-groups?orgId=1&var-period=m&var-repogroup_name=All) 프로젝트는 쿠버네티스와 여러 서브프로젝트의 진행 속도에 관한 흥미로운 데이터 지점을 집계합니다.

여기에는 개인의 기여부터 기여하는 회사 수까지 모든 것이 포함되며, 이 생태계를 발전시키는 데 들어가는
노력의 깊이와 폭을 보여줍니다.

2026년 5월 18일부터 2026년 8월 26일까지 15주 동안 진행된 v1.37 릴리스 주기에 쿠버네티스 기여는 최대 212개 회사와 1,754명에 이르렀습니다.

이 데이터의 출처는 다음과 같습니다.

- [쿠버네티스에 기여한 회사](https://k8s.devstats.cncf.io/d/11/companies-contributing-in-repository-groups?orgId=1&from=1779058800000&to=1787781600000&var-period=d28&var-repogroup_name=All&var-repo_name=kubernetes%2Fkubernetes)
- [전체 생태계 기여](https://k8s.devstats.cncf.io/d/11/companies-contributing-in-repository-groups?orgId=1&from=1779055200000&to=1787781600000%20&var-period=d28&var-repogroup_name=All&var-repo_name=kubernetes%2Fkubernetes)

여기서 기여란 커밋, 코드 리뷰, 코멘트, 이슈 또는 PR 생성, 블로그와 문서를 포함한 PR 리뷰,
이슈 및 PR에 대한 코멘트를 뜻합니다.

기여에 관심이 있다면 [시작하기](https://www.kubernetes.dev/docs/guide/#getting-started)
페이지를 확인합니다.

### 이벤트 소식

전 세계에서 열릴 KubeCon을 확인하세요.

- [KubeCon + CloudNativeCon China](https://www.lfopensource.cn/kubecon-cloudnativecon-openinfra-summit-pytorch-conference-china/):
  2026년 9월 7~9일, 중국 상하이
- [KubeCon + CloudNativeCon North America](https://events.linuxfoundation.org/kubecon-cloudnativecon-north-america/):
  2026년 11월 9~12일, 미국 솔트레이크시티

2026년 남은 기간에 열릴 쿠버네티스 커뮤니티 데이(Kubernetes Community Days, KCD)를 확인하세요.

#### 2026년 9월

- [KCD x Ceph x OpenInfra Day Korea](https://community2.cncf.io/events/details/cncf-kcd-south-korea-presents-kcd-x-ceph-x-openinfra-day-korea-2026/):
  2026년 9월 1일, 대한민국 서울
- [KCD San Francisco Bay Area](https://community2.cncf.io/events/details/cncf-kcd-sf-bay-area-presents-kcd-san-francisco-bay-area-2026/):
  2026년 9월 1일, 미국 마운틴뷰
- [KCD Washington DC](https://community2.cncf.io/events/details/cncf-kcd-washington-dc-presents-kcd-washington-dc-2026/):
  2026년 9월 15일, 미국 워싱턴 DC
- [KCD Gujarat](https://community2.cncf.io/events/details/cncf-kcd-gujarat-presents-kcd-gujarat-2026/):
  2026년 9월 19일, 인도 아마다바드
- [KCD São Paulo](https://community2.cncf.io/events/details/cncf-kcd-brasil-presents-kcd-sao-paulo-2026/):
  2026년 9월 26일, 브라질 상파울루
- [KCD Sofia](https://community2.cncf.io/events/details/cncf-kcd-sofia-presents-kubernetes-community-days-sofia-2026/):
  2026년 9월 29일, 불가리아 소피아

#### 2026년 10월

- [KCD UK – Edinburgh](https://community2.cncf.io/events/details/cncf-kcd-uk-presents-kubernetes-community-days-uk-edinburgh-2026/):
  2026년 10월 19~20일, 영국 에든버러
- [KCD Nigeria](https://community2.cncf.io/events/details/cncf-kcd-nigeria-presents-kcd-nigeria-2026-telling-the-african-cloud-native-story/):
  2026년 10월 24일, 나이지리아 라고스

#### 2026년 11월

- [KCD Porto](https://community2.cncf.io/events/details/cncf-kcd-porto-presents-kcd-porto-2026-collab-with-devops-days-portugal/):
  2026년 11월 19~20일, 포르투갈 포르투
- [KCD Hangzhou](https://sessionize.com/kcd-hangzhou-2026/):
  2026년 11월 28일, 중국 항저우

#### 2026년 12월

- [KCD Suisse Romande](https://community2.cncf.io/events/details/cncf-kcd-suisse-romande-presents-kcd-suisse-romande-2026/):
 2026년 12월 9~10일, 스위스 메이랭
- [KCD Provence](https://community2.cncf.io/events/details/cncf-kcd-provence-presents-kcd-provence-2026/):
 2026년 12월 10일, 프랑스 엑상프로방스
- [KCD Florida – Miami](https://community2.cncf.io/events/details/cncf-kcd-florida-presents-kcd-florida-2026-miami/):
  2026년 12월 11일, 미국 마이애미

최신 이벤트 세부 정보는 [CNCF 이벤트 페이지](https://community2.cncf.io/events/#/list)에서 확인할 수 있습니다.

### 다가오는 릴리스 웨비나

2026년 9월 23일 수요일 오후 4시(UTC)에 쿠버네티스 v1.37 릴리스 팀 구성원과 함께 이번 릴리스의 주요 내용을 알아보세요. 자세한 정보와 등록 방법은 [CNCF 온라인 프로그램 사이트의 이벤트 페이지](https://community2.cncf.io/events/details/cncf-cncf-online-programs-presents-cloud-native-live-kubernetes-v137-webinar/)에서 확인합니다.


## 참여 방법

쿠버네티스에 참여하는 가장 간단한 방법은 관심 분야와 일치하는 여러 [특별 관심 그룹(Special Interest Group, SIG)](https://kubernetes.dev/community/community-groups/sigs/) 중 하나에 참여하는 것입니다.

어디서 시작해야 할지 모르겠다면 매월 열리는 [신규 기여자 오리엔테이션](https://www.kubernetes.dev/docs/orientation/)에 참여합니다.
여기에서 프로젝트 구조를 설명하고 첫 번째 기여 방법을 안내합니다.

- [쿠버네티스 기여자](https://www.kubernetes.dev/docs/guide/)가 되는 방법 알아보기
- 쿠버네티스 [블로그](https://kubernetes.io/blog/)에서 최신 소식 읽기
- [Slack](http://slack.k8s.io/) 참여하기
- 최신 소식을 위해 [Bluesky](https://bsky.app/profile/kubernetes.io) 팔로우하기
- [LinkedIn](https://www.linkedin.com/company/kubernetes/) 팔로우하기
- [X](https://x.com/kubernetesio) 팔로우하기
- [Discuss](https://discuss.kubernetes.io/)에서 커뮤니티 논의에 참여하기
- [Stack Overflow](http://stackoverflow.com/questions/tagged/kubernetes)에 질문을 올리거나 답변하기
- [쿠버네티스 최종 사용자 사례](https://www.cncf.io/case-studies/) 공유하기
- [쿠버네티스 릴리스 팀](https://github.com/kubernetes/sig-release/tree/master/release-team)에 대해 더 알아보기
