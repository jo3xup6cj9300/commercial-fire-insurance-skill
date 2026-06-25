# Commercial Fire Quote Rules

## Property Schedule

Use these insured-property categories:

- 建築物
- 營業裝修
- 機器設備
- 營業生財
- 貨物

Each insured location should include name/code, address, amounts, repair-shop flag when relevant, building structure, and a per-location subtotal.

The fire total is the sum of all location subtotals.

## "含..." Parsing

Allow users to enter combined descriptions directly in amount fields, such as:

- `38000000(含建築物)` in 營業裝修
- `400000(含機器設備)` in 營業生財

Output behavior:

- Keep the amount in the field where the user typed it.
- Preserve the user's parenthetical text on that amount.
- In the included field, show `含<source field label>`.

Example:

Input:

- 營業生財 = `400000(含機器設備)`

Output:

- 機器設備 = `含營業生財`
- 營業生財 = `400,000(含機器設備)`

## Additional Covers

Default additional cover list:

- 地震險
- 颱風及洪水險
- 罷工、暴動、民眾騷擾、惡意破壞行為險
- 自動消防裝置滲漏險
- 竊盜險
- 第三人意外責任險
- 水漬險
- 爆炸險
- 航空器墜落、機動車輛碰撞險
- 營業中斷險(製造業適用)
- 營業中斷險(非製造業適用)
- 煙燻險
- 地層下陷、滑動或山崩險
- 租金損失險
- 恐怖主義險

商火險 is the base policy and must not appear as an additional cover.

## Catastrophe and Other Additional Cover Logic

Catastrophe covers:

- Names containing 颱風 or 洪水
- Names containing 地震

Other additional covers:

- All selected additional covers that are not catastrophe covers.

Output:

- 天災保額: `火險保額 X%：amount`
- 天災限額: `火險保額 X%：amount`
- 附加險: group other additional covers by effective percentage.

When all other additional covers use the default percentage:

- Output one row: `其他附加險比例`

When percentages differ:

- Group covers by percentage.
- The largest group should be summarized as `除<exception names>外，其餘附加險種`.
- Smaller groups should list their cover names joined by `、`.

Example:

- 爆炸險, 水漬險 = 50%
- All other additional covers = 70%

Output:

- `爆炸險、水漬險：火險保額 50%：54,000,000`
- `除爆炸險、水漬險外，其餘附加險種：火險保額 70%：75,600,000`

## Insured Perils

Place this before 標的物與保額:

- 火災
- 爆炸引起之火災
- 閃電雷擊

## SB Endorsement Clauses

The tool should:

- Recommend SB clauses based on selected insured property categories.
- Keep the clause list fully expanded in the input area.
- Hide internal parser notes from users.
- Allow custom user-added endorsement clauses.
- Output selected SB clauses and custom clauses together.

Clause title cleanup:

- Remove English parenthetical names.
- Preserve Chinese parenthetical text.
- Remove incomplete trailing English parenthetical fragments.
