#BI

# Tableau

- https://sfabi.lottewellfood.com/
## 매출 현황
| Name | URI | Screen ID | api id |
| ---- | ---- | ---- | ---- |
| 영업조직 | views/_17037462075910/- |  | api.bi.salesStatus.salesForce |
| 거래처 | views/_17037462075910/-_1 |  | api.bi.salesStatus.salesCust |
| 카테고리 | views/_17037462075910/-_2 |  | api.bi.salesStatus.salesCategory |
| 체인/영업조직 | views/_17037462075910/-_3 |  | api.bi.salesStatus.salesChain |
| 브랜드 | views/_17037462075910/-_4 |  | api.bi.salesStatus.salesBrand |
| SKU | views/_17037462075910/-SKU | TRPT_0131 | api.bi.salesStatus.salesSKU |

## 매출채권 분석
| Name | URI | api id |
| ---- | ---- | ---- |
| 영업조직,영업사원(현황) | views/_17032340841490/sheet0 | api.bi.tradeReceivable.curSalesForce |
| 영업조직,영업사원(추이) | views/_17032340841490/sheet1 | api.bi.tradeReceivable.transSalesForce |
| 거래처(현황) | views/_17032340841490/sheet2 | api.bi.tradeReceivable.curSalesCust |
| 거래처(추이) | views/_17032340841490/sheet3 | api.bi.tradeReceivable.transSalesCust |

## 반품 분석
| Name | URI |  | api id |
| ---- | ---- | ---- | ---- |
| 영업조직/영업사원 | views/_0/sheet0 | TRPT_0210 | api.bi.returnReport.salesForce |
| 카테고리 | views/_0/sheet1 | TRPT_0220 | api.bi.returnReport.salesCategory |

## 영업 월보
| Name | URI | api id |
| ---- | ---- | ---- |
| 영업조직 | views/_17037446413430/sheet0 |  |
| 영업사원 | views/_17037446413430/sheet1 |  |
| 거래처 분류 | views/_17037446413430/sheet2 |  |
| 체인 | views/_17037446413430/sheet3 |  |
| 영업사원,거래처 | views/_17037446413430/sheet4 |  |

## 영업 일보
| Name | URI | Screen ID | api id |
| ---- | ---- | ---- | ---- |
| 영업조직 | views/_17035755428990/sheet0 |  | api.bi.salesDaily.salesForce |
| 영업사원 | views/_17035755428990/sheet1 | TRPT_0110 | api.bi.salesDaily.salesPerson |
| 거래처 분류 | views/_17035755428990/sheet2 | TRPT_0120 | api.bi.salesDaily.salesCust |
| 체인 | views/_17035755428990/sheet3 |  | api.bi.salesDaily.salesChain |
| 영업사원,거래처 | views/_17035755428990/sheet4 | TRPT_0111, | api.bi.salesDaily.salesPersonByCust |
