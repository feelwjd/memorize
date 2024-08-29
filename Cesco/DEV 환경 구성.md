
# 환경 정보

## bizMOB

- 서비스 배포 주소
	- [Portal] https://bizmob-portal.cfapps.ap12.hana.ondemand.com/smart-admin/index.sm
	- [Appstore] https://bizmob-appstore.cfapps.ap12.hana.ondemand.com/appstore/
	- [Server] https://bizmob-mobile-server.cfapps.ap12.hana.ondemand.com/cesco-server-web/

## Github

- URL
	- https://github.com/Cesco-NGTF
- Token
```
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
```

## CF CLI

- cf login
- bizmob-mobile-server connect ssl postgresql
```bash
cf ssh -L localhost:1763:postgres-927704b1-d3e3-41bd-8464-134dd03ff332.cu2h3ll9ayju.ap-northeast-2.rds.amazonaws.com:1763 bizmob-mobile-server -N
```


## S3 Object Store
```bash
aws s3 ls s3://hcp-9cf99965-d47c-476b-9e00-c7c44074d199
```

