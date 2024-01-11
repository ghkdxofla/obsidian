# Abstract
- [[AWS OpenSearch]] 운영 시, 참고하면 좋은 지표들의 목록
- 지표를 통해 모니터링하고, 운영 시 트러블 슈팅을 진행
# Content
## 지표
### 기본
- 샤드에 대한 상태
	- 완전 관리형 서비스여서 특정 노드에 프라이머리 샤드나 레플리카 샤드가 편중되었을 경우 `relocation` 기능을 사용할 수 없어 리밸런싱 필요
- 노드 별 용량
- CPU, Memory, JVM, GC, Disk I/O, Latency, Threads, Heap
- 노드 별 샤드 분표율
### CloudWatch
- 다음 [링크](https://docs.aws.amazon.com/ko_kr/opensearch-service/latest/developerguide/managedomains-cloudwatchmetrics.html#managedomains-cloudwatchmetrics-cluster-metrics) 에서 상세 지표 확인 후 설정 가능
- 각 지표에 🚨 표시를 통해 주요 지표를 나타냈음
    
- 클러스터 지표
    
    |지표|설명|
    |---|---|
    |ClusterStatus.green 🚨|값이 1이면 클러스터의 노드에 모든 인덱스 샤드가 할당되었음을 나타냅니다. 관련 통계: Maximum|
    |ClusterStatus.yellow 🚨|값이 1이면 모든 인덱스의 기본 샤드가 클러스터의 노드에 할당되어 있지만 하나 이상의 인덱스에 대해 복제본 샤드가 할당되어 있지 않음을 나타냅니다. 자세한 내용은 [https://docs.aws.amazon.com/ko_kr/opensearch-service/latest/developerguide/handling-errors.html#handling-errors-yellow-cluster-status](https://docs.aws.amazon.com/ko_kr/opensearch-service/latest/developerguide/handling-errors.html#handling-errors-yellow-cluster-status) 섹션을 참조하세요.|
    |관련 통계: Maximum||
    |[http://ClusterStatus.red](http://ClusterStatus.red) 🚨|값이 1이면 인덱스 하나 이상의 기본 및 복제본 샤드가 클러스터의 노드에 할당되지 않았음을 나타냅니다. 자세한 내용은 [https://docs.aws.amazon.com/ko_kr/opensearch-service/latest/developerguide/handling-errors.html#handling-errors-red-cluster-status](https://docs.aws.amazon.com/ko_kr/opensearch-service/latest/developerguide/handling-errors.html#handling-errors-red-cluster-status) 섹션을 참조하세요.|
    |관련 통계: Maximum||
    |Shards.active 🚨|활성 기본 및 복제본 샤드의 총 수입니다.|
    |관련 통계: Maximum, Sum||
    |Shards.unassigned|클러스터의 노드에 할당되지 않은 샤드 수입니다.|
    |관련 통계: Maximum, Sum||
    |Shards.delayedUnassigned 🚨|제한 시간 설정으로 노드 할당이 지연된 샤드 수입니다.|
    |관련 통계: Maximum, Sum||
    |Shards.activePrimary 🚨|활성 기본 샤드 수입니다.|
    |관련 통계: Maximum, Sum||
    |Shards.initializing 🚨|초기화 중인 샤드 수입니다.|
    |관련 통계: 합계||
    |Shards.relocating 🚨|재배치 중인 샤드 수입니다.|
    |관련 통계: 합계||
    |Nodes|전용 프라이머리 노드 및 UltraWarm 노드를 포함하여 OpenSearch Service 클러스터에 있는 노드 수입니다. 자세한 내용은 [https://docs.aws.amazon.com/ko_kr/opensearch-service/latest/developerguide/managedomains-configuration-changes.html](https://docs.aws.amazon.com/ko_kr/opensearch-service/latest/developerguide/managedomains-configuration-changes.html) 섹션을 참조하세요.|
    |관련 통계: Maximum||
    |SearchableDocuments|클러스터의 모든 데이터 노드에서 검색 가능한 총 문서 수입니다.|
    |관련 통계: 최소, 최대, 평균||
    |DeletedDocuments|클러스터의 모든 데이터 노드에서 삭제 표시된 총 문서 수입니다. 이들 문서는 더 이상 검색 결과에 나타나지 않지만, OpenSearch는 세그먼트 병합 시에만 삭제된 문서를 디스크에서 제거합니다. 이 지표는 삭제 요청 후 증가하고 세그먼트 병합 후 감소합니다.|
    |관련 통계: 최소, 최대, 평균||
    |CPUUtilization 🚨|클러스터의 데이터 노드에 대한 CPU 사용량 백분율입니다. 최대는 CPU 사용량이 가장 높은 노드를 나타냅니다. 평균은 클러스터의 모든 노드를 나타냅니다. 이 지표는 개별 노드에도 사용할 수 있습니다.|
    |관련 통계: Maximum, Average||
    |FreeStorageSpace 🚨|클러스터에서 사용할 수 있는 데이터 노드 공간입니다. Sum은 클러스터의 사용 가능한 전체 공간을 표시하지만, 정확한 값을 얻으려면 이 기간을 1분으로 두어야 합니다. Minimum, Maximum은 사용 가능한 공간이 가장 작은 노드와 가장 큰 노드를 각각 표시합니다. 이 지표는 개별 노드에도 사용할 수 있습니다. OpenSearch Service는 이 지표가 0에 도달하는 경우 ClusterBlockException를 발생시킵니다. 복구하려면 인덱스를 삭제하거나, 더 큰 인스턴스를 추가하거나 기존 인스턴스에 EBS 기반 스토리지를 추가해야 합니다. 자세한 내용은 [https://docs.aws.amazon.com/ko_kr/opensearch-service/latest/developerguide/handling-errors.html#handling-errors-watermark](https://docs.aws.amazon.com/ko_kr/opensearch-service/latest/developerguide/handling-errors.html#handling-errors-watermark) 섹션을 참조하세요.|
    |OpenSearch Service 콘솔은 이 값을 GiB로 표시합니다. Amazon CloudWatch 콘솔은 이 값을 MiB로 표시합니다.||
    |참고||
    |FreeStorageSpace는 항상 OpenSearch _cluster/stats 및 _cat/allocation API가 제공하는 값보다 낮습니다. OpenSearch Service는 내부 작업을 위해 각 인스턴스에 스토리지 공간의 일정 비율을 예약합니다. 자세한 내용은 [https://docs.aws.amazon.com/ko_kr/opensearch-service/latest/developerguide/sizing-domains.html#bp-storage을](https://docs.aws.amazon.com/ko_kr/opensearch-service/latest/developerguide/sizing-domains.html#bp-storage%EC%9D%84) 참조하세요.||
    |관련 통계: Minimum, Maximum, Average, Sum||
    |ClusterUsedSpace 🚨|클러스터의 총 사용 공간입니다. 정확한 값을 얻으려면 이 기간을 1분으로 두어야 합니다.|
    |OpenSearch Service 콘솔은 이 값을 GiB로 표시합니다. Amazon CloudWatch 콘솔은 이 값을 MiB로 표시합니다.||
    |관련 통계: Minimum, Maximum||
    |ClusterIndexWritesBlocked 🚨|수신되는 쓰기 요청에 대한 클러스터의 허용 또는 차단 여부를 나타냅니다. 값이 0이면 클러스터가 요청을 허용하고 있다는 것을 의미합니다. 값이 1이면 클러스터가 요청을 차단하고 있다는 것을 의미합니다.|
    |몇 가지 공통적인 요인을 꼽자면 FreeStorageSpace가 너무 낮은 경우 또는 JVMMemoryPressure가 너무 높은 경우가 있습니다. 이러한 문제를 줄이려면 디스크 공간을 추가하거나 클러스터를 확장하는 것이 좋습니다.||
    |관련 통계: Maximum||
    |JVMMemoryPressure 🚨|클러스터의 모든 데이터 노드에 사용된 Java 힙의 최대 비율입니다. OpenSearch Service는 Java 힙에 인스턴스 RAM의 절반을 사용합니다(최대 힙 크기 32GiB). 인스턴스를 최대 64GiB의 RAM까지 수직 확장할 수 있으며 인스턴스를 추가하면 수평 확장도 가능합니다. [https://docs.aws.amazon.com/ko_kr/opensearch-service/latest/developerguide/cloudwatch-alarms.html](https://docs.aws.amazon.com/ko_kr/opensearch-service/latest/developerguide/cloudwatch-alarms.html) 섹션을 참조하세요.|
    |관련 통계: Maximum||
    |참고||
    |서비스 소프트웨어 R20220323에서 이 지표에 대한 로직이 변경되었습니다. 자세한 내용은 [https://docs.aws.amazon.com/ko_kr/opensearch-service/latest/developerguide/release-notes.html를](https://docs.aws.amazon.com/ko_kr/opensearch-service/latest/developerguide/release-notes.html%EB%A5%BC) 참조하세요.||
    |OldGenJVMMemoryPressure 🚨|클러스터의 모든 데이터 노드에서 '구세대'에 사용된 Java 힙의 최대 비율입니다. 이 지표는 노드 수준에도 사용할 수 있습니다.|
    |관련 통계: Maximum||
    |AutomatedSnapshotFailure|클러스터에 대해 실패한 자동 스냅샷 수입니다. 값 1은 지난 36시간 동안 도메인에 대해 생성된 자동 스냅샷이 없음을 나타냅니다.|
    |관련 통계: Minimum, Maximum||
    |CPUCreditBalance|클러스터의 데이터 노드에 사용할 수 있는 잔여 CPU 크레딧입니다. CPU 크레딧은 1분 동안 CPU 코어의 전체 성능을 제공합니다. 자세한 내용은 Amazon EC2 개발자 안내서의 [https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/burstable-credits-baseline-concepts.html을](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/burstable-credits-baseline-concepts.html%EC%9D%84) 참조하세요. 이 지표는 T2 인스턴스 유형에 대해서만 확인할 수 있습니다.|
    |관련 통계: Minimum||
    |OpenSearchDashboardsHealthyNodes 🚨|OpenSearch Dashboards의 상태 확인입니다. 최솟값, 최댓값 및 평균이 모두 1과 같으면 Dashboards가 정상적으로 동작하고 있습니다. 최대 1, 최소 0, 평균 0.7인 노드가 10개 있는 경우 이는 노드 7개(70%)가 정상이고 노드 3개(30%)가 비정상임을 의미합니다.|
    |관련 통계: 최소, 최대, 평균||
    |OpensearchDashboardsReportingFailedRequestSysErrCount|서버 문제 또는 기능 제한으로 인해 실패한 OpenSearch Dashboards 보고서 생성에 대한 요청 수입니다.|
    |관련 통계: 합계||
    |OpensearchDashboardsReportingFailedRequestUserErrCount|클라이언트 문제로 인해 실패한 OpenSearch Dashboards 보고서 생성에 대한 요청 수입니다.|
    |관련 통계: 합계||
    |OpensearchDashboardsReportingRequestCount|OpenSearch Dashboards 보고서 생성에 대한 총 요청 수입니다.|
    |관련 통계: 합계||
    |OpensearchDashboardsReportingSuccessCount|OpenSearch Dashboards 보고서 생성에 대해 성공한 요청 수입니다.|
    |관련 통계: 합계||
    |KMSKeyError|값 1은 저장 데이터를 암호화하는 데 사용된 AWS KMS 키가 비활성화된 것을 나타냅니다. 도메인을 정상 작동으로 복원하려면 키를 다시 활성화해야 합니다. 콘솔에는 저장된 데이터를 암호화하는 도메인에 대해서만 이 지표가 표시됩니다.|
    |관련 통계: Minimum, Maximum||
    |KMSKeyInaccessible|값 1은 저장된 데이터를 암호화하는 데 사용된 AWS KMS 키가 삭제되었거나 OpenSearch Service에 대한 권한 부여가 취소되었음을 나타냅니다. 이 상태의 도메인은 복원할 수 없습니다. 하지만 수동 스냅샷이 있는 경우 해당 스냅샷을 사용하여 도메인의 데이터를 새 도메인으로 마이그레이션할 수 있습니다. 콘솔에는 저장된 데이터를 암호화하는 도메인에 대해서만 이 지표가 표시됩니다.|
    |관련 통계: Minimum, Maximum||
    |InvalidHostHeaderRequests 🚨|잘못된(또는 누락된) 호스트 헤더를 포함하여 OpenSearch 클러스터에 수행된 HTTP 요청 수입니다. 유효한 요청에는 도메인 호스트 이름이 호스트 헤더 값으로 포함됩니다. OpenSearch Service는 제한적인 액세스 정책이 없는 퍼블릭 액세스 도메인에 대한 잘못된 요청을 거부합니다. 모든 도메인에 제한적인 액세스 정책을 적용하는 것을 권장합니다.|
    |이 지표에 대한 값이 클 경우, 사용자의 OpenSearch 클라이언트가 요청에 도메인 호스트 이름이(예를 들어, IP 주소 아님) 포함되었는지 확인합니다.||
    |관련 통계: 합계||
    |OpenSearchRequests(previously 🚨ElasticsearchRequests)|OpenSearch 클러스터에 수행된 요청 수입니다.|
    |관련 통계: 합계||
    |2xx, 3xx, 4xx, 5xx 🚨|해당 HTTP 응답 코드(2xx, 3xx, 4xx, 5xx)를 발생시킨 도메인에 대한 요청 건수입니다.|
    |관련 통계: 합계||
    |ThroughputThrottle 🚨|디스크가 제한되었는지 여부를 나타냅니다. 제한은 ReadThroughputMicroBursting 및 WriteThroughputMicroBursting의 총 처리량이 최대 처리량 MaxProvisionedThroughput보다 높을 때 발생합니다. MaxProvisionedThroughput는 인스턴스 처리량 또는 프로비저닝된 볼륨 처리량 중 더 낮은 값입니다. 값이 1이면 디스크가 제한되었음을 나타냅니다. 값이 0이면 정상적인 동작 상태를 나타냅니다.|
    |인스턴스 처리량에 대한 자세한 내용은 [https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-optimized.html를](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-optimized.html%EB%A5%BC) 참조하세요. 볼륨 처리량에 대한 자세한 내용은 [http://aws.amazon.com/ebs/volume-types/을](http://aws.amazon.com/ebs/volume-types/%EC%9D%84) 참조하십시오.||
    |관련 통계: Minimum, Maximum||
    
- 전용 프라이머리 노드 지표
    
    |지표|설명|
    |---|---|
    |MasterCPUUtilization 🚨|전용 프라이머리 노드에서 사용하는 최대 CPU 리소스 비율. 이 지표가 60%에 도달하면 인스턴스 유형의 크기를 늘리는 것이 좋습니다.|
    |관련 통계: Maximum||
    |MasterFreeStorageSpace 🚨|이 지표는 관련이 없으므로 무시해도 좋습니다. 이 서비스에서는 프라이머리 노드를 데이터 노드로 사용하지 않습니다.|
    |MasterJVMMemoryPressure 🚨|클러스터의 모든 전용 프라이머리 노드에 사용되는 Java 힙의 최대 비율. 이 지표가 85%에 도달하면 더 큰 인스턴스 유형으로 이전하는 것이 좋습니다.|
    |관련 통계: Maximum||
    |참고||
    |서비스 소프트웨어 R20220323에서 이 지표에 대한 로직이 변경되었습니다. 자세한 내용은 [https://docs.aws.amazon.com/ko_kr/opensearch-service/latest/developerguide/release-notes.html를](https://docs.aws.amazon.com/ko_kr/opensearch-service/latest/developerguide/release-notes.html%EB%A5%BC) 참조하세요.||
    |MasterOldGenJVMMemoryPressure 🚨|프라이머리 노드당 '구세대'에 사용된 Java 힙의 최대 비율입니다.|
    |관련 통계: Maximum||
    |MasterCPUCreditBalance|클러스터의 전용 프라이머리 노드에 사용할 수 있는 잔여 CPU 크레딧입니다. CPU 크레딧은 1분 동안 CPU 코어의 전체 성능을 제공합니다. 자세한 내용은 Amazon EC2 개발자 안내서의 [https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/burstable-credits-baseline-concepts.html을](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/burstable-credits-baseline-concepts.html%EC%9D%84) 참조하세요. 이 지표는 T2 인스턴스 유형에 대해서만 확인할 수 있습니다.|
    |관련 통계: Minimum||
    |MasterReachableFromNode 🚨|MasterNotDiscovered 예외에 대한 상태 확인입니다. 값이 1이면 정상적인 동작 상태를 나타냅니다. 값이 0이면 /_cluster/health/가 오류를 일으킨 것을 나타냅니다.|
    |여기에서 오류란 소스 노드에서 프라이머리 노드에 도달할 수 없다는 것을 의미합니다. 이러한 오류가 발생하는 이유는 대부분 네트워크 연결 문제 또는 AWS 종속성 문제에서 기인합니다.||
    |관련 통계: Maximum||
    |MasterSysMemoryUtilization 🚨|사용 중인 프라이머리 노드 메모리의 비율입니다.|
    |관련 통계: Maximum||
    
- EBS 볼륨 지표
    
    |지표|설명|
    |---|---|
    |ReadLatency 🚨|EBS 볼륨에 대한 읽기 작업의 대기 시간(초)입니다. 이 지표는 개별 노드에도 사용할 수 있습니다.|
    |관련 통계: 최소, 최대, 평균||
    |WriteLatency 🚨|EBS 볼륨에 대한 쓰기 작업의 대기 시간(초)입니다. 이 지표는 개별 노드에도 사용할 수 있습니다.|
    |관련 통계: 최소, 최대, 평균||
    |ReadThroughput 🚨|EBS 볼륨에 대한 읽기 작업의 처리량(바이트/초)입니다. 이 지표는 개별 노드에도 사용할 수 있습니다.|
    |관련 통계: 최소, 최대, 평균||
    |ReadThroughputMicroBursting|[https://repost.aws/knowledge-center/ebs-identify-micro-bursting을](https://repost.aws/knowledge-center/ebs-identify-micro-bursting%EC%9D%84) 고려할 때 EBS 볼륨의 읽기 작업 처리량(초당 바이트)입니다. 이 지표는 개별 노드에도 사용할 수 있습니다. 마이크로 버스팅은 EBS 볼륨이 상당히 짧은 시간(1분 미만) 동안 높은 IOPS 또는 처리량을 버스팅할 때 발생합니다.|
    |관련 통계: 최소, 최대, 평균||
    |WriteThroughput 🚨|EBS 볼륨에 대한 쓰기 작업의 처리량(바이트/초)입니다. 이 지표는 개별 노드에도 사용할 수 있습니다.|
    |관련 통계: 최소, 최대, 평균||
    |WriteThroughputMicroBursting|[https://repost.aws/knowledge-center/ebs-identify-micro-bursting을](https://repost.aws/knowledge-center/ebs-identify-micro-bursting%EC%9D%84) 고려할 때 EBS 볼륨의 쓰기 작업 처리량(초당 바이트)입니다. 이 지표는 개별 노드에도 사용할 수 있습니다. 마이크로 버스팅은 EBS 볼륨이 상당히 짧은 시간(1분 미만) 동안 높은 IOPS 또는 처리량을 버스팅할 때 발생합니다.|
    |관련 통계: 최소, 최대, 평균||
    |DiskQueueDepth 🚨|EBS 볼륨에 대해 대기 중인 I/O 요청 수입니다.|
    |관련 통계: 최소, 최대, 평균||
    |ReadIOPS 🚨|EBS 볼륨에 대한 읽기 작업의 초당 I/O 작업 수입니다. 이 지표는 개별 노드에도 사용할 수 있습니다.|
    |관련 통계: 최소, 최대, 평균||
    |ReadIOPSMicroBursting|[https://repost.aws/knowledge-center/ebs-identify-micro-bursting을](https://repost.aws/knowledge-center/ebs-identify-micro-bursting%EC%9D%84) 고려할 때 EBS 볼륨에 대한 읽기 작업의 초당 I/O 작업 수입니다. 이 지표는 개별 노드에도 사용할 수 있습니다. 마이크로 버스팅은 EBS 볼륨이 상당히 짧은 시간(1분 미만) 동안 높은 IOPS 또는 처리량을 버스팅할 때 발생합니다.|
    |관련 통계: 최소, 최대, 평균||
    |WriteIOPS 🚨|EBS 볼륨에 대한 쓰기 작업의 초당 I/O 작업 수입니다. 이 지표는 개별 노드에도 사용할 수 있습니다.|
    |관련 통계: 최소, 최대, 평균||
    |WriteIOPSMicroBursting|[https://repost.aws/knowledge-center/ebs-identify-micro-bursting을](https://repost.aws/knowledge-center/ebs-identify-micro-bursting%EC%9D%84) 고려할 때 EBS 볼륨에 대한 쓰기 작업의 초당 I/O 작업 수입니다. 이 지표는 개별 노드에도 사용할 수 있습니다. 마이크로 버스팅은 EBS 볼륨이 상당히 짧은 시간(1분 미만) 동안 높은 IOPS 또는 처리량을 버스팅할 때 발생합니다.|
    |관련 통계: 최소, 최대, 평균||
    |BurstBalance|EBS 볼륨에 대해 버스트 버킷에 남아 있는 입력 및 출력(I/O) 크레딧의 비율입니다. 값이 100이면 볼륨에 최대 크레딧 수가 누적되었음을 의미합니다. 이 비율이 70% 미만으로 떨어지면 [https://docs.aws.amazon.com/ko_kr/opensearch-service/latest/developerguide/handling-errors.html#handling-errors-low-ebs-burst](https://docs.aws.amazon.com/ko_kr/opensearch-service/latest/developerguide/handling-errors.html#handling-errors-low-ebs-burst) 섹션을 참조하세요. gp3 볼륨 유형이 있는 도메인과 볼륨 크기가 1000GiB를 초과하는 gp2 볼륨이 있는 도메인의 경우 버스트 균형은 0으로 유지됩니다.|
    |관련 통계: 최소, 최대, 평균||
    
- 인스턴스 지표
    
    |지표|설명|
    |---|---|
    |IndexingLatency 🚨|한 노드의 모든 인덱싱 작업에 소요된 총 시간 차이(밀리초)로, 이 차이는 분 N에서 (N-1)분입니다.|
    |관련 노드 통계: Average||
    |관련 클러스터 통계: Average, Maximum||
    |IndexingRate 🚨|분당 인덱싱 작업 수입니다. 2개의 문서를 추가하고 2개를 4개 작업으로 업데이트하는 _bulk API에 대한 하나의 호출입니다. 이것은 하나 이상의 노드에 분산될 수 있습니다. 인덱스에 하나 이상의 복제본이 있는 경우 클러스터의 다른 노드 역시 총 4개의 인덱싱 작업을 기록합니다. 문서 삭제는 이 지표에 포함되지 않습니다.|
    |관련 노드 통계: Average||
    |관련 클러스터 통계: Average, Maximum, Sum||
    |SearchLatency 🚨|한 노드의 모든 검색 작업에 소요된 총 시간 차이(밀리초)로, 이 차이는 분 N에서 (N-1)분입니다.|
    |관련 노드 통계: Average||
    |관련 클러스터 통계: Average, Maximum||
    |SearchRate 🚨|한 데이터 노드의 모든 샤드에 대한 분당 검색 요청의 총 수입니다. _search API에 대한 단일 호출은 많은 샤드로부터 결과를 반환할 수 있습니다. 이러한 샤드 중 5개가 한 노드에 있는 경우, 클라이언트가 단 한 개만 요청했더라도 노드는 이 지표에 대해 5를 보고할 것입니다.|
    |관련 노드 통계: Average||
    |관련 클러스터 통계: Average, Maximum, Sum||
    |SegmentCount 🚨|데이터 노드의 세그먼트 수입니다. 세그먼트가 많을수록 각 검색 시간이 길어집니다. OpenSearch는 때때로 작은 세그먼트를 더 큰 세그먼트로 병합합니다.|
    |관련 노드 통계: Maximum, Average||
    |관련 클러스터 통계: Sum, Maximum, Average||
    |SysMemoryUtilization 🚨|사용 중인 인스턴스 메모리의 비율(%)입니다. 이 지표의 값이 큰 것은 정상이며 일반적으로 클러스터에 문제가 있음을 나타내지 않습니다. 잠재적인 성능 및 안정성 문제에 대한 더 나은 지표는 JVMMemoryPressure 지표를 참조하세요.|
    |관련 노드 통계: Minimum, Maximum, Average||
    |관련 클러스터 통계: Minimum, Maximum, Average||
    |JVMGCYoungCollectionCount 🚨|"신세대" 가비지 수집이 실행된 횟수입니다. 클러스터 작업은 일반적으로 실행 수가 계속 증가하여 커집니다.|
    |관련 노드 통계: Maximum||
    |관련 클러스터 통계: Sum, Maximum, Average||
    |JVMGCYoungCollectionTime 🚨|클러스터가 "신세대" 가비지 수집을 수행하는 데 소비 한 시간(밀리초)입니다.|
    |관련 노드 통계: Maximum||
    |관련 클러스터 통계: Sum, Maximum, Average||
    |JVMGCOldCollectionCount 🚨|"구세대" 가비지 수집이 실행된 횟수입니다. 리소스가 충분한 클러스터에서는 이 수가 적게 유지되고 자주 증가하지 않습니다.|
    |관련 노드 통계: Maximum||
    |관련 클러스터 통계: Sum, Maximum, Average||
    |JVMGCOldCollectionTime 🚨|클러스터가 "구세대" 가비지 수집을 수행하는 데 소비 한 시간 (밀리초)입니다.|
    |관련 노드 통계: Maximum||
    |관련 클러스터 통계: Sum, Maximum, Average||
    |OpenSearchDashboardsConcurrentConnections|OpenSearch Dashboards에 대한 활성 동시 연결 수입니다. 이 수가 계속 증가하면 클러스터 확장을 고려합니다.|
    |관련 노드 통계: Maximum||
    |관련 클러스터 통계: Sum, Maximum, Average||
    |OpenSearchDashboardsHealthyNode|개별 OpenSearch Dashboards 노드에 대한 상태 확인입니다. 값이 1이면 정상적인 동작 상태를 나타냅니다. 값이 0이면 Dashboards에 액세스할 수 없다는 것을 나타냅니다.|
    |관련 노드 통계: Minimum||
    |관련 클러스터 통계: Minimum, Maximum, Average||
    |OpenSearchDashboardsHeapTotal|OpenSearch Dashboards에 할당된 힙 메모리 양(MiB)입니다. 다른 EC2 인스턴스 유형은 정확한 메모리 할당에 영향을 줄 수 있습니다.|
    |관련 노드 통계: Maximum||
    |관련 클러스터 통계: Sum, Maximum, Average||
    |OpenSearchDashboardsHeapUsed|OpenSearch Dashboards에서 사용하는 힙 메모리의 절대 양(MiB)입니다.|
    |관련 노드 통계: Maximum||
    |관련 클러스터 통계: Sum, Maximum, Average||
    |OpenSearchDashboardsHeapUtilization|OpenSearch Dashboards에서 사용하는 사용 가능한 힙 메모리의 최대 백분율입니다. 이 값이 80% 이상으로 증가하면 클러스터 확장을 고려합니다.|
    |관련 노드 통계: Maximum||
    |관련 클러스터 통계: Minimum, Maximum, Average||
    |OpenSearchDashboardsOS1MinuteLoad|OpenSearch Dashboards에 대한 1분 CPU 로드 평균입니다. CPU 로드는 이상적으로 1.00 미만으로 유지되어야 합니다. 일시적인 급증은 정상이지만 이 지표가 지속해서 1.00을 초과할 경우 인스턴스 유형의 크기를 늘리는 것이 좋습니다.|
    |관련 노드 통계: Average||
    |관련 클러스터 통계: Average, Maximum||
    |OpenSearchDashboardsRequestTotal|OpenSearch Dashboards에 대한 총 HTTP 요청 수입니다. 시스템 속도가 느리거나 Dashboards 요청 수가 많으면 인스턴스 유형의 크기를 늘리는 것을 고려합니다.|
    |관련 노드 통계: Sum||
    |관련 클러스터 통계: Sum||
    |OpenSearchDashboardsResponseTimesMaxInMillis|OpenSearch Dashboards가 요청에 응답하는 데 걸리는 최대 시간(밀리초)입니다. 요청 결과가 반환되는 데 시간이 지속해서 오래 걸리는 경우 인스턴스 유형의 크기를 늘리는 것을 고려합니다.|
    |관련 노드 통계: Maximum||
    |관련 클러스터 통계: Maximum, Average||
    |SearchTaskCancelled|코디네이터 노드 취소 횟수.|
    |관련 노드 통계: Sum||
    |관련 클러스터 통계: Sum||
    |SearchShardTaskCancelled|데이터 노드 취소 횟수.|
    |관련 노드 통계: Sum||
    |관련 클러스터 통계: Sum,||
    |ThreadpoolForce_mergeQueue 🚨|강제 병합 스레드 풀에서 대기 중인 작업의 수입니다. 대기열 크기가 지속해서 높으면 클러스터 확장을 고려합니다.|
    |관련 노드 통계: Maximum||
    |관련 클러스터 통계: Sum, Maximum, Average||
    |ThreadpoolForce_mergeRejected 🚨|강제 병합 스레드 풀에서 거부된 작업의 수입니다. 이 수가 계속 증가하면 클러스터 확장을 고려합니다.|
    |관련 노드 통계: Maximum||
    |관련 클러스터 통계: Sum||
    |ThreadpoolForce_mergeThreads 🚨|강제 병합 스레드 풀의 크기입니다.|
    |관련 노드 통계: Maximum||
    |관련 클러스터 통계: Average, Sum||
    |ThreadpoolIndexQueue 🚨|인덱스 스레드 풀에서 대기 중인 작업의 수입니다. 대기열 크기가 지속해서 높으면 클러스터 확장을 고려합니다. 인덱스 대기열의 최대 크기는 200입니다.|
    |관련 노드 통계: Maximum||
    |관련 클러스터 통계: Sum, Maximum, Average||
    |ThreadpoolIndexRejected 🚨|인덱스 스레드 풀에서 거부된 작업의 수입니다. 이 수가 계속 증가하면 클러스터 확장을 고려합니다.|
    |관련 노드 통계: Maximum||
    |관련 클러스터 통계: Sum||
    |ThreadpoolIndexThreads 🚨|인덱스 스레드 풀의 크기입니다.|
    |관련 노드 통계: Maximum||
    |관련 클러스터 통계: Average, Sum||
    |ThreadpoolSearchQueue 🚨|검색 스레드 풀에서 대기 중인 작업의 수입니다. 대기열 크기가 지속해서 높으면 클러스터 확장을 고려합니다. 검색 대기열의 최대 크기는 1,000입니다.|
    |관련 노드 통계: Maximum||
    |관련 클러스터 통계: Sum, Maximum, Average||
    |ThreadpoolSearchRejected 🚨|검색 스레드 풀에서 거부된 작업의 수입니다. 이 수가 계속 증가하면 클러스터 확장을 고려합니다.|
    |관련 노드 통계: Maximum||
    |관련 클러스터 통계: Sum||
    |ThreadpoolSearchThreads 🚨|검색 스레드 풀의 크기입니다.|
    |관련 노드 통계: Maximum||
    |관련 클러스터 통계: Average, Sum||
    |Threadpoolsql-workerQueue 🚨|SQL 검색 스레드 풀에서 대기 중인 작업의 수입니다. 대기열 크기가 지속해서 높으면 클러스터 확장을 고려합니다.|
    |관련 노드 통계: Maximum||
    |관련 클러스터 통계: Sum, Maximum, Average||
    |Threadpoolsql-workerRejected 🚨|SQL 검색 스레드 풀에서 거부된 작업의 수입니다. 이 수가 계속 증가하면 클러스터 확장을 고려합니다.|
    |관련 노드 통계: Maximum||
    |관련 클러스터 통계: Sum||
    |Threadpoolsql-workerThreads 🚨|SQL 검색 스레드 풀의 크기입니다.|
    |관련 노드 통계: Maximum||
    |관련 클러스터 통계: Average, Sum||
    |ThreadpoolBulkQueue|벌크 스레드 풀에서 대기 중인 작업의 수입니다. 대기열 크기가 지속해서 높으면 클러스터 확장을 고려합니다.|
    |관련 노드 통계: Maximum||
    |관련 클러스터 통계: Sum, Maximum, Average||
    |ThreadpoolBulkRejected|벌크 스레드 풀에서 거부된 작업의 수입니다. 이 수가 계속 증가하면 클러스터 확장을 고려합니다.|
    |관련 노드 통계: Maximum||
    |관련 클러스터 통계: Sum||
    |ThreadpoolBulkThreads|벌크 스레드 풀의 크기입니다.|
    |관련 노드 통계: Maximum||
    |관련 클러스터 통계: Average, Sum||
    |ThreadpoolWriteThreads 🚨|쓰기 스레드 풀의 크기입니다.|
    |관련 노드 통계: Maximum||
    |관련 클러스터 통계: Average, Sum||
    |ThreadpoolWriteQueue|쓰기 스레드 풀에서 대기 중인 작업의 수입니다.|
    |관련 노드 통계: Maximum||
    |관련 클러스터 통계: Average, Sum||
    |ThreadpoolWriteRejected 🚨|쓰기 스레드 풀에서 거부된 작업의 수입니다.|
    |관련 노드 통계: Maximum||
    |관련 클러스터 통계: Average, Sum||
    |참고||
    |버전 7.1에서는 기본 쓰기 대기열 크기가 200에서 10000으로 증가했기 때문에 이 지표는 더 이상 OpenSearch Service에서 거부하는 유일한 지표가 아닙니다. CoordinatingWriteRejected, PrimaryWriteRejected, ReplicaWriteRejected 지표를 사용하여 7.1 및 이후 버전에서 거부를 모니터링합니다.||
    |CoordinatingWriteRejected 🚨|마지막 OpenSearch Service 프로세스 시작 이후 인덱싱 압력으로 인해 조정 노드에서 발생한 총 거부 횟수입니다.|
    |관련 노드 통계: Maximum||
    |관련 클러스터 통계: Average, Sum||
    |이 지표는 버전 7.1 및 이후 버전에서 사용할 수 있습니다.||
    |PrimaryWriteRejected 🚨|마지막 OpenSearch Service 프로세스 시작 이후 인덱싱 압력으로 인해 기본 샤드에서 발생한 총 거부 횟수입니다.|
    |관련 노드 통계: Maximum||
    |관련 클러스터 통계: Average, Sum||
    |이 지표는 버전 7.1 및 이후 버전에서 사용할 수 있습니다.||
    |ReplicaWriteRejected 🚨|마지막 OpenSearch Service 프로세스 시작 이후 인덱싱 압력으로 인해 복제본 샤드에서 발생한 총 거부 횟수입니다.|
    |관련 노드 통계: Maximum||
    |관련 클러스터 통계: Average, Sum||
    |이 지표는 버전 7.1 및 이후 버전에서 사용할 수 있습니다.||
    
- 알림 지표
    
    |지표|설명|
    |---|---|
    |AlertingDegraded 🚨|값이 1이면 알림 인덱스가 빨간색이거나 하나 이상의 노드가 일정에 따라 실행되지 않음을 의미하고, 값이 0이면 정상적인 동작 상태를 나타냅니다.|
    |관련 통계: Maximum||
    |AlertingIndexExists|값이 1이면 .opensearch-alerting-config 인덱스가 존재함을 의미하고, 값이 0이면 존재하지 않음을 의미합니다. 알림 기능을 처음 사용할 때까지 이 값은 0으로 유지됩니다.|
    |관련 통계: Maximum||
    |[http://AlertingIndexStatus.green](http://AlertingIndexStatus.green) 🚨|인덱스의 상태입니다. 값이 1이면 녹색을 의미하고, 값이 0이면 인덱스가 존재하지 않거나 녹색이 아님을 의미합니다.|
    |관련 통계: Maximum||
    |[http://AlertingIndexStatus.red](http://AlertingIndexStatus.red) 🚨|인덱스의 상태입니다. 값이 1이면 빨간색을 의미하고, 값이 0이면 인덱스가 존재하지 않거나 빨간색이 아님을 의미합니다.|
    |관련 통계: Maximum||
    |AlertingIndexStatus.yellow 🚨|인덱스의 상태입니다. 값이 1이면 노란색을 의미하고, 값이 0이면 인덱스가 존재하지 않거나 노란색이 아님을 의미합니다.|
    |관련 통계: Maximum||
    |AlertingNodesNotOnSchedule 🚨|값이 1이면 일부 작업이 일정에 따라 실행되고 있지 않음을 의미하고, 값이 0이면 모든 알림 작업이 일정에 따라 실행 중이거나 알림 작업이 없음을 의미합니다. OpenSearch Service 콘솔을 점검하거나 _nodes/stats 요청을 실행하여 리소스 사용량이 높은 노드가 있는지 확인합니다.|
    |관련 통계: Maximum||
    |AlertingNodesOnSchedule|값이 1이면 모든 알림 작업이 일정에 따라 실행 중이거나 알림 작업이 없음을 의미하고, 값이 0이면 일부 작업이 일정에 따라 실행되고 있지 않음을 의미합니다.|
    |관련 통계: Maximum||
    |AlertingScheduledJobEnabled|값이 1이면 opensearch.scheduled_jobs.enabled 클러스터 설정이 true임을 의미하고, 값이 0이면 false이며 예약된 작업이 비활성화되었음을 의미합니다.|
    |관련 통계: Maximum||
    
- 이상 탐지 지표
    
    |지표|설명|
    |---|---|
    |ADPluginUnhealthy 🚨|값이 1이면 실패 횟수가 많거나 사용하는 인덱스 중 하나가 빨간색이기 때문에 이상 탐지 플러그 인이 제대로 작동하지 않음을 의미합니다. 값이 0이면 플러그인이 예상대로 작동하고 있음을 나타냅니다.|
    |관련 통계: Maximum||
    |ADExecuteRequestCount|이상을 탐지하기 위한 요청 수입니다.|
    |관련 통계: 합계||
    |ADExecuteFailureCount 🚨|이상을 탐지하기 위한 실패한 요청 수입니다.|
    |관련 통계: 합계||
    |ADHCExecuteFailureCount 🚨|높은 카디널리티 탐지기를 위한 이상 탐지 요청 중 실패한 요청 수입니다.|
    |관련 통계: 합계||
    |ADHCExecuteRequestCount|높은 카디널리티 탐지기를 위한 이상 탐지 요청 수입니다.|
    |관련 통계: 합계||
    |ADAnomalyResultsIndexStatusIndexExists|값이 1이면 .opensearch-anomaly-results 별칭이 가리키는 인덱스가 존재함을 의미합니다. 이상 탐지를 처음 사용할 때까지 이 값은 0으로 유지됩니다.|
    |관련 통계: Maximum||
    |ADAnomalyResultsIndexStatus.red|값이 1이면 .opensearch-anomaly-results 별칭이 가리키는 인덱스가 빨간색임을 의미합니다. 값이 0이면 그렇지 않음을 의미합니다. 이상 탐지를 처음 사용할 때까지 이 값은 0으로 유지됩니다.|
    |관련 통계: Maximum||
    |ADAnomalyDetectorsIndexStatusIndexExists|값이 1이면 .opensearch-anomaly-detectors 인덱스가 존재함을 의미하고, 값이 0이면 존재하지 않음을 의미합니다. 이상 탐지를 처음 사용할 때까지 이 값은 0으로 유지됩니다.|
    |관련 통계: Maximum||
    |ADAnomalyDetectorsIndexStatus.red|값이 1이면 .opensearch-anomaly-detectors 인덱스가 빨간색임을 의미합니다. 값이 0이면 그렇지 않음을 의미합니다. 이상 탐지를 처음 사용할 때까지 이 값은 0으로 유지됩니다.|
    |관련 통계: Maximum||
    |ADModelsCheckpointIndexStatusIndexExists|값이 1이면 .opensearch-anomaly-checkpoints 인덱스가 존재함을 의미하고, 값이 0이면 존재하지 않음을 의미합니다. 이상 탐지를 처음 사용할 때까지 이 값은 0으로 유지됩니다.|
    |관련 통계: Maximum||
    |ADModelsCheckpointIndexStatus.red|값이 1이면 .opensearch-anomaly-checkpoints 인덱스가 빨간색임을 의미합니다. 값이 0이면 그렇지 않음을 의미합니다. 이상 탐지를 처음 사용할 때까지 이 값은 0으로 유지됩니다.|
    |관련 통계: Maximum||
    
- Multi-AZ with Standby 지표
    
    여기서 볼 수 있는 지표가 최소로 필요한 지표의 기준이 될 수 있음
    
    |지표|설명|
    |---|---|
    |CPUUtilization 🚨|클러스터의 데이터 노드에 대한 CPU 사용량 백분율입니다. 최대는 CPU 사용량이 가장 높은 노드를 나타냅니다. 평균은 클러스터의 모든 노드를 나타냅니다. 이 지표는 개별 노드에도 사용할 수 있습니다.|
    |FreeStorageSpace 🚨|클러스터에서 사용할 수 있는 데이터 노드 공간입니다. Sum은 클러스터의 사용 가능한 전체 공간을 표시하지만, 정확한 값을 얻으려면 이 기간을 1분으로 두어야 합니다. Minimum, Maximum은 사용 가능한 공간이 가장 작은 노드와 가장 큰 노드를 각각 표시합니다. 이 지표는 개별 노드에도 사용할 수 있습니다. OpenSearch Service는 이 지표가 0에 도달하는 경우 ClusterBlockException를 발생시킵니다. 복구하려면 인덱스를 삭제하거나, 더 큰 인스턴스를 추가하거나 기존 인스턴스에 EBS 기반 스토리지를 추가해야 합니다. 자세한 내용은 [https://docs.aws.amazon.com/ko_kr/opensearch-service/latest/developerguide/handling-errors.html#handling-errors-watermark](https://docs.aws.amazon.com/ko_kr/opensearch-service/latest/developerguide/handling-errors.html#handling-errors-watermark) 섹션을 참조하세요.|
    |OpenSearch Service 콘솔은 이 값을 GiB로 표시합니다. Amazon CloudWatch 콘솔은 이 값을 MiB로 표시합니다.||
    |JVMMemoryPressure 🚨|클러스터의 모든 데이터 노드에 사용된 Java 힙의 최대 비율입니다. OpenSearch Service는 Java 힙에 인스턴스 RAM의 절반을 사용합니다(최대 힙 크기 32GiB). 인스턴스를 최대 64GiB의 RAM까지 수직 확장할 수 있으며 인스턴스를 추가하면 수평 확장도 가능합니다. [https://docs.aws.amazon.com/ko_kr/opensearch-service/latest/developerguide/cloudwatch-alarms.html](https://docs.aws.amazon.com/ko_kr/opensearch-service/latest/developerguide/cloudwatch-alarms.html) 섹션을 참조하세요.|
    |SysMemoryUtilization 🚨|사용 중인 인스턴스 메모리의 비율(%)입니다. 이 지표의 값이 큰 것은 정상이며 일반적으로 클러스터에 문제가 있음을 나타내지 않습니다. 잠재적인 성능 및 안정성 문제에 대한 더 나은 지표는 JVMMemoryPressure 지표를 참조하세요.|
    |IndexingLatency 🚨|한 노드의 모든 인덱싱 작업에 소요된 총 시간 차이(밀리초)로, 이 차이는 분 N에서 (N-1)분입니다.|
    |IndexingRate 🚨|분당 인덱싱 작업 수입니다.|
    |SearchLatency 🚨|한 노드의 모든 검색 작업에 소요된 총 시간 차이(밀리초)로, 이 차이는 분 N에서 (N-1)분입니다.|
    |SearchRate 🚨|한 데이터 노드의 모든 샤드에 대한 분당 검색 요청의 총 수입니다.|
    |ThreadpoolSearchQueue 🚨|검색 스레드 풀에서 대기 중인 작업의 수입니다. 대기열 크기가 지속해서 높으면 클러스터 확장을 고려합니다. 검색 대기열의 최대 크기는 1,000입니다.|
    |ThreadpoolWriteQueue 🚨|쓰기 스레드 풀에서 대기 중인 작업의 수입니다.|
    |ThreadpoolSearchRejected 🚨|검색 스레드 풀에서 거부된 작업의 수입니다. 이 수가 계속 증가하면 클러스터 확장을 고려합니다.|
    |ThreadpoolWriteRejected 🚨|쓰기 스레드 풀에서 거부된 작업의 수입니다.|
    
- SQL 지표
    
    |지표|설명|
    |---|---|
    |SQLFailedRequestCountByCusErr 🚨|클라이언트 문제로 인해 실패한 _sql API에 대한 요청 수입니다. 예를 들어 IndexNotFoundException으로 인해 요청이 HTTP 상태 코드 400을 반환할 수 있습니다.|
    |관련 통계: 합계||
    |SQLFailedRequestCountBySysErr 🚨|서버 문제 또는 기능 제한으로 인해 실패한, _sql API에 대한 요청 수입니다. 예를 들어 VerificationException으로 인해 요청이 HTTP 상태 코드 503을 반환할 수 있습니다.|
    |관련 통계: 합계||
    |SQLRequestCount 🚨|_sql API 요청 수입니다.|
    |관련 통계: 합계||
    |SQLDefaultCursorRequestCount|SQLRequestCount와 유사하지만 페이지 매김 요청만 계산합니다.|
    |관련 통계: 합계||
    |SQLUnhealthy 🚨|값이 1이면 특정 요청에 대한 응답으로 SQL 플러그인이 5xx 응답 코드를 반환하거나 잘못된 쿼리 DSL을 OpenSearch에 전달함을 나타냅니다. 다른 요청은 계속 성공합니다. 값이 0이면 최근 실패가 없음을 나타냅니다. 지속해서 값이 1이면 클라이언트가 플러그인에 수행하는 요청 문제를 해결합니다.|
    |관련 통계: Maximum||
    
- 클러스터 간 검색 지표
    
    |지표|차원|설명|
    |---|---|---|
    |CrossClusterOutboundConnections|ConnectionId|연결된 노드 수입니다. 응답에 하나 이상의 건너뛴 도메인이 포함된 경우 이 지표를 사용하여 비정상 연결을 추적합니다. 이 숫자가 0으로 떨어지면 연결이 비정상입니다.|
    |CrossClusterOutboundRequests|ConnectionId|대상 도메인으로 전송된 검색 요청 수입니다. 클러스터 간 검색 요청의 부하가 도메인에 너무 부담되는지 확인하고 이 지표의 스파이크와 JVM/CPU 스파이크의 상관관계를 분석하는 데 사용합니다.|
    
- 클러스터 간 복제 지표
    
    |지표|설명|
    |---|---|
    |ReplicationRate 🚨|초당 평균 복제 작업 속도. 이 지표는 IndexingRate 지표와 유사합니다.|
    |LeaderCheckPoint 🚨|특정 연결에 대한 모든 복제 인덱스에 걸친 리더 체크포인트의 합계입니다. 이 지표를 사용하여 복제 대기 시간을 측정할 수 있습니다.|
    |FollowerCheckPoint 🚨|특정 연결에 대한 모든 복제 인덱스에 걸친 팔로어 체크포인트의 합계입니다. 이 지표를 사용하여 복제 대기 시간을 측정할 수 있습니다.|
    |ReplicationNumSyncingIndices|복제 상태가 SYNCING인 인덱스의 수입니다.|
    |ReplicationNumBootstrappingIndices|복제 상태가 BOOTSTRAPPING인 인덱스의 수입니다.|
    |ReplicationNumPausedIndices|복제 상태가 PAUSED인 인덱스의 수입니다.|
    |ReplicationNumFailedIndices|복제 상태가 FAILED인 인덱스의 수입니다.|
    |AutoFollowNumSuccessStartReplication|특정 연결에 대한 복제 규칙에 의해 성공적으로 생성된 팔로어 인덱스의 수입니다.|
    |AutoFollowNumFailedStartReplication 🚨|일치하는 패턴이 있을 때 복제 규칙에 의해 생성되지 못한 팔로어 인덱스의 수입니다. 이 문제는 원격 클러스터의 네트워크 문제 또는 보안 문제(즉, 연결된 역할에 복제를 시작할 권한이 없음)로 인해 발생할 수 있습니다.|
    |AutoFollowLeaderCallFailure 🚨|새 데이터를 가져오기 위해 팔로어 인덱스에서 리더 인덱스로의 쿼리가 실패했는지 여부입니다. 값 1은 최근 1분 동안 1회 이상의 실패한 호출이 있음을 의미합니다.|
## 이슈 시 대응할 요소
- 데이터 노드가 `shutdown` 됐을 경우, 중지 기간 내 발생한 인덱스 추가, 수정 필요
## 알림 구성
### 설정
- 기본적으로 [[OpenSearch Dashboards]] 를 통해서 설정 가능
1. OpenSearch Dashboards 기본 메뉴에서 **Alerting**(알림)을 선택하고 **Create monitor**(모니터 생성)를 선택합니다.
2. 쿼리별, 버킷별, 클러스터별 지표 또는 문서별 모니터를 생성합니다. 지침은 [모니터 생성](https://opensearch.org/docs/latest/monitoring-plugins/alerting/monitors/#create-a-monitor)을 참조하세요.
3. **Triggers**(트리거)의 경우 하나 이상의 트리거를 생성합니다. 지침은 [트리거 생성](https://opensearch.org/docs/latest/monitoring-plugins/alerting/monitors/#create-triggers)을 참조하세요.
4. **Actions**(작업)의 경우 알림에 대한 [notification channel](https://docs.aws.amazon.com/ko_kr/opensearch-service/latest/developerguide/alerting.html#alerting-notifications)(알림 채널)을 설정합니다. Slack, Amazon Chime, 사용자 지정 Webhook 또는 SNS 중에서 선택할 수 있습니다. 알림을 받으려면 채널에 연결되어야 합니다. 예를 들어 OpenSearch Service 도메인이 인터넷에 연결하여 Slack 채널을 알리거나 사용자 지정 Webhook을 타사 서버로 보낼 수 있어야 합니다. 사용자 지정 Webhook에 알림을 보내려면 OpenSearch Service 도메인에 퍼블릭 IP 주소가 있어야 합니다.

# Reference
- [후기 서비스 AWS Opensearch 도입기](https://helloworld.kurly.com/blog/2023-review-opensearch/)
- [Amazon OpenSearch Service의 알림 구성](https://docs.aws.amazon.com/ko_kr/opensearch-service/latest/developerguide/alerting.html)
- [Amazon CloudWatch로 OpenSearch 클러스터 지표 모니터링](https://docs.aws.amazon.com/ko_kr/opensearch-service/latest/developerguide/managedomains-cloudwatchmetrics.html)