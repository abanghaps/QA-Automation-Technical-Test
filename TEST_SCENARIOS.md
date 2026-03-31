# API Test Scenarios - JSONPlaceholder

Dokumen ini berisi skenario pengujian komprehensif untuk 3 endpoint utama menggunakan pendekatan **Positive**, **Negative**, dan **Edge Case**.

## 1. Endpoint: GET /posts
| Type | ID | Scenario Description | Expected Result |
| :--- | :--- | :--- | :--- |
| **Positive** | P1-01 | Valid request returns 200 OK | Status 200 OK & Response < 500ms |
| **Positive** | P1-02 | JSON Schema Validation | Response berupa Array dengan key lengkap |
| **Positive** | P1-03 | Data Integrity (Uniqueness) | Tidak ada ID yang duplikat dalam list |
| **Positive** | P1-04 | Header Content-Type Check | Header mengandung application/json |
| **Negative** | N1-01 | Invalid Resource Path | Status 404 Not Found |
| **Negative** | N1-02 | Unsupported HTTP Method | Status 405 atau 404 |
| **Negative** | N1-03 | Invalid Query Param Data Type | Status 400 atau data diabaikan (safe) |
| **Negative** | N1-04 | Access without Authentication | Status 401 (Jika API diproteksi) |
| **Edge Case** | E1-01 | High Frequency Request (Flooding) | Server stabil / Rate Limit 429 |
| **Edge Case** | E1-02 | Large Response Payload Size | Data diterima lengkap (100 items) |
| **Edge Case** | E1-03 | Incompatible Accept Header | Status 406 atau tetap return JSON |
| **Edge Case** | E1-04 | Empty State Simulation | Return empty array [] bukan 404 |

## 2. Endpoint: GET /posts/{id}
| Type | ID | Scenario Description | Expected Result |
| :--- | :--- | :--- | :--- |
| **Positive** | P2-01 | BVA: Lower Boundary (ID: 1) | Status 200 OK & Data valid |
| **Positive** | P2-02 | BVA: Upper Boundary (ID: 100) | Status 200 OK & Data valid |
| **Positive** | P2-03 | Object Structure Integrity | Response berupa Object (bukan Array) |
| **Positive** | P2-04 | Content Consistency Validation | Data title/body tidak kosong |
| **Negative** | N2-01 | ID Not Found (ID: 101) | Status 404 Not Found |
| **Negative** | N2-02 | Negative ID Value (ID: -1) | Status 404 Not Found |
| **Negative** | N2-03 | SQL Injection Attempt | Status 404 atau 400 (Sanitized) |
| **Negative** | N2-04 | Data Type Mismatch (String ID) | Status 404 Not Found |
| **Edge Case** | E2-01 | Very Large Integer (Overflow) | Status 404 Not Found |
| **Edge Case** | E2-02 | Zero Leading ID (ID: 001) | Sistem mengonversi ke 1 atau 404 |
| **Edge Case** | E2-03 | Character Special in URL | Status 404 Not Found |
| **Edge Case** | E2-04 | Trailing Slash Handling | Status 200 OK atau Redirect |

## 3. Endpoint: POST /posts
| Type | ID | Scenario Description | Expected Result |
| :--- | :--- | :--- | :--- |
| **Positive** | P3-01 | Valid Resource Creation | Status 201 Created & New ID 101 |
| **Positive** | P3-02 | UTF-8 Character Support | Data tersimpan dengan simbol/emoji |
| **Positive** | P3-03 | Data Reflection Validation | Body request sama dengan body response |
| **Positive** | P3-04 | Optional Fields Submission | Status 201 Created |
| **Negative** | N3-01 | Missing Required Field: title | Status 400 Bad Request |
| **Negative** | N3-02 | Missing Required Field: body | Status 400 Bad Request |
| **Negative** | N3-03 | Strict Typing: userId as string | Status 400 Bad Request |
| **Negative** | N3-04 | Malformed JSON Syntax | Status 400 Bad Request |
| **Edge Case** | E3-01 | Empty Body Payload `{}` | Status 400 Bad Request (Current: 201) |
| **Edge Case** | E3-02 | XSS Injection Attempt | Script disimpan sebagai plain text |
| **Edge Case** | E3-03 | Payload Size Stress Test | Status 413 Payload Too Large |
| **Edge Case** | E3-04 | Duplicate Key in Payload | Konsistensi data (ambil key terakhir) |
