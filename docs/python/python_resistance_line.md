---
tags:
  - Python
---

# 上値の抵抗線(レジスタンスライン)を起点としたトレード

FX取引では、相場の上昇を阻む水準となるラインを上値の抵抗線やレジスタンスラインと呼ぶ

このラインは過去の高値区域に設定されることが多く、上値を押し上げる力が弱まる領域と考えられてる

## レジスタンスラインが形成されるメカニズム
過去の相場高値は参入した投資家の損切りラインとなりやすく、再度その水準を試すと売りが優勢となる可能性が高い

また、特定の水準を上下に持ち直す動きが繰り返されると、その水準が心理的な抵抗となり上値抵抗線が形成されやすくなる

## レジスタンスラインの役割
レジスタンスラインは主に以下のような役割がある

### 上値の節目となる水準を示す
相場の上値を押し上げにくい節目の目安<br>
投資家はこの水準到達時の動向を注視することが多くなる

### 売り圧力の強まる領域を示す
この水準では過去の売りが優勢になった痕跡があるため、売り手の意識する水準となる<br>
上値の重要な節目

### トレンド反転の兆候を示す
レジスタンスラインで上値が重心を形成し始めると、トレンド反転の兆候となりえる<br>
上昇力が緩慢になる重要な点

### 目標水準となる
相場がレジスタンスを上回ることは買いの確認材料となり、上値目標の積み上がりを支持する

## レジスタンスラインの活用法
レジスタンスラインは主に以下のように活用することができる

- 上値の重要節目を把握できる
- 売り圧力が高まる領域を認識できる
- 反転兆候の出現を察知できる
- 目標水準を設定しやすくなる
- エントリーチャンスを見極めやすくなる

つまり、レジスタンスラインを把握することで相場の節目が見えてくるため、売買判断を行う上で非常に有効なポイントとなる

上昇相場ではこのラインの突破が買いシグナルとなるなど、活用法は状況によって変化する

## レジスタンスライン突破の意味
レジスタンスラインの突破は、以下のような意味がある

- 上値の重要な節目を上回ったことを示す
- 上昇トレンドが強まったことの兆候
- さらなる上昇余地があることのシグナル
- 売り圧力が弱まったことの証左
- 買いシグナルとなる場合が多い

したがって、レジスタンス突破は上値の節目を上回り、強気トレンドが継続していることを示す動きと言える

新規買い参入の好機となりやすいサインの1つとなる

## Pythonでレジスタンスラインを定義
数理的に上値抵抗線を定義する

関数上での抵抗線の定義は以下のとおり

- 指定した期間の終値データから極大値を抽出する
- 抽出した極大値を中心に一定の範囲を設定する(buffer変数で範囲を指定)
- 設定した範囲内で価格が一定回数(rebound_thresholdで指定)上下に振れた場合、その範囲を上値抵抗帯と判断する
- 上記の条件を満たす範囲を上値抵抗線として出力する


つまり、

- 局地的な最大値周辺
- 一定範囲の価格帯
- 所定の回数、上下に価格が振れること

という3つの条件を満たす場合に、その価格帯を上値抵抗線として定義する

```py
def calculate_resistance_zone(df, start, end, buffer=1, rebound_threshold=2):

    data = df['close'].iloc[start:end+1].values
    maxima_indices, _ = find_peaks(data)
    maxima_values = data[maxima_indices]
    resistance_zones = []

    for value in maxima_values:
        upper_bound = value + buffer
        lower_bound = value - buffer
        rebound_count = np.sum(( lower_bound < data) & (data < upper_bound))

        if rebound_count >= rebound_threshold:
            resistance_zones.append((lower_bound, upper_bound))

    return resistance_zones
```