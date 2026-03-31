# Evidence Level Definitions v2.0 / 證據分級定義
# Universal standard — category-independent / 通用標準 — 與品類無關

> Last updated / 最後更新: 2026-03-31
> Derived from / 來源: spec/evidence-levels.md v1.0

---

## Level 1: Verifiable Hard Data / 可驗證硬資料（最高可信度）

**Source types / 來源類型:**
- Official manufacturer manuals, service manuals, white papers / 原廠官方手冊、維修手冊、白皮書
- Public statements by original engineers or designers (with clear attribution) / 原廠工程師或設計者的公開發言（有明確出處）
- Peer-reviewed academic papers (AES, EURASIP, IEEE, etc.) / 同儕審查學術論文
- Independent laboratory test reports (with methodology) / 獨立實驗室測試報告（附量測方法說明）
- Patent documents (USPTO, EPO, WIPO) / 專利文件

**Supported claim strength / 可支撐的主張強度:**
- Precise specification numbers / 精確規格數字
- Design rationale for architecture and component selection / 電路架構與元件選用的設計理由
- Exact version timelines and serial number ranges / 確切的版本時間線與序號範圍
- Material composition and manufacturing process details / 材料成分與製造工藝的具體說明

**Citation requirements / 引用格式要求:**
- Must include URL or document name + page number / 必須附 URL 或文件名稱 + 頁碼
- Must pass Phase 1.5 URL audit / 必須經過 Phase 1.5 URL 審計
- For PDFs: note acquisition source (official site / scan / third-party archive) / PDF 需標明取得來源

**Uncertainty trigger / 不確定性觸發:**
- If L1 sources contradict each other (e.g., two official documents with different numbers), both must be reported with possible explanations (version differences, measurement conditions). Do NOT pick one as the sole correct answer.
- 若 L1 來源之間出現數字矛盾，必須在章節內明確標出矛盾並說明可能原因，不得自行選一個數字當成唯一正確答案。

---

## Level 2: Semi-Official Professional Reviews / 半正式專業評論（高可信度）

**Source types / 來源類型:**
- Major industry publications with technical measurements / 含量測的業界大型媒體
- Named engineers in industry media interviews or bylined articles / 具名工程師在業界媒體的專訪或署名文章
- Manufacturer-authorized supplementary documentation / 製造商授權的使用者指南補充文件

**Supported claim strength / 可支撐的主張強度:**
- Common subjective characteristics (requires multiple L2 sources to state as "widely recognized") / 常見主觀特徵描述（需多篇 L2 來源一致才可陳述為「普遍認可」）
- Typical use cases and pairing recommendations / 典型應用情境與搭配建議
- Semi-technical descriptions of version differences (if measurement data exists) / 版本差異的半技術說明（若有量測數據佐證）

**Citation requirements / 引用格式要求:**
- Must include URL + author name + publication date / 必須附 URL + 作者姓名 + 發布日期
- If multiple L2 sources disagree, all must be reported separately / 若多篇 L2 來源說法不一，必須分別陳述

**Uncertainty trigger / 不確定性觸發:**
- Only one L2 source supports a claim / 僅有一篇 L2 來源支持某主張
- Source published > 10 years ago without subsequent confirmation / 來源發布超過 10 年且未有後續確認
- Measurement equipment or methodology not described / 量測設備或方法未說明

---

## Level 3: Professional Community Consensus / 專業社群共識（中等可信度）

**Source types / 來源類型:**
- Long-running, high-engagement technical discussion threads led by named professionals / 長期高互動、由具名專業人士主導的技術討論串
- User discussions with measurements / 含量測的用戶討論
- Named professionals' blogs or social media posts (with traceable identity) / 具名專業人士的部落格或社群貼文

**Supported claim strength / 可支撐的主張強度:**
- User experience trends among professionals / 多數專業人士的使用經驗趨勢
- Common failure modes (collective impression) / 常見故障模式的集體印象
- Community evaluation of modification procedures / 改裝程序的社群評價

**Citation requirements / 引用格式要求:**
- Must include URL + thread title + poster ID (or real name) + approximate date / 必須附 URL + 討論串標題 + 發言者 ID + 大約日期
- Must append "(community consensus, not measurement-verified)" to cited statements / 引用時必須標注「（社群共識，非量測驗證）」

**Uncertainty trigger / 不確定性觸發:**
- Only L3 sources support a technical claim / 僅有 L3 來源支持某技術主張
- Discussion older than 5 years without follow-up verification / 社群討論超過 5 年且無後續驗證
- Significant disagreement within the same forum / 同一論壇內有明顯的意見分歧

---

## Level 4: General Content / 一般內容（低可信度，僅作佐證）

**Source types / 來源類型:**
- General blogs, personal WordPress/Medium articles / 一般部落格、個人文章
- Non-professional YouTube reviews / 非具名業界人士的 YouTube 評測
- E-commerce product copy / 電商產品文案
- Unattributed wiki entries / 未具名的 wiki 條目
- Social media posts / 社群媒體貼文

**Supported claim strength / 可支撐的主張強度:**
- Only for supplementing "emotional color" or "public perception" / 僅可用來補充「情緒色彩」或「大眾認知印象」
- Cannot independently support any technical claim / 不可單獨支撐任何技術性主張
- Cannot override L1-L3 conclusions / 不可用來否定 L1–L3 的結論

**Citation requirements / 引用格式要求:**
- Must explicitly label "(Level 4, for reference only, no technical verification)" / 必須明確標注「（Level 4，僅供參考，不具技術驗證效力）」

---

## Cross-Level Usage Rules / 跨等級使用規則

| Claim Type / 主張類型 | Minimum Level / 最低等級 | Notes / 備註 |
|---|---|---|
| Precise technical specs / 精確技術規格 | L1 | Cannot substitute with L2 or below / 不得用 L2 以下替代 |
| Design rationale / 設計理由 | L1-L2 | L2 requires technical measurements / L2 需有技術量測 |
| Version timeline / 版本時間線 | L1 | If L1 insufficient, mark as speculative / 若不足標明為推測 |
| Subjective descriptions / 主觀描述 | L2-L3 | Requires multi-source agreement / 需多來源一致 |
| Market pricing / 市場價格 | L2-L3 | Must include query date / 需附查詢日期 |
| Cultural narratives / 文化敘述 | L2-L4 | Must label source level and subjectivity / 標注來源等級與主觀性 |

## Downgrade Rules / 等級降級規則

- L1 source with unclear document version or unofficial scan → downgrade to L2 / L1 文件版本不明或非官方掃描 → 降為 L2
- L2 source lacking measurement data, subjective only → downgrade to L3 / L2 缺乏量測數據 → 降為 L3
- L2 source with unverifiable author identity → downgrade to L3 / L2 作者身份無法核實 → 降為 L3
- Any source failing URL audit (404 or content mismatch) → downgrade to L4, must replace / URL 審計失效 → 降為 L4，需替換
