# Pedestrian Traffic Light

## 考えるべきこと

* 早朝・夕方/昼間/夜間
* 晴天/曇天/雨天
* 逆光/手ブレ
* カメラレンズの汚れ・濡れ（雨の水滴）
* カメラの仰角や方位の誘導
* 青信号の残り時間/青信号の点滅/赤->青への切り替わり
* 信号機の背景にある赤/青の発光看板
* 車両用信号（丸/矢印）の除去
* 車両の方向指示器やテールランプの除去
* 進行方向とは異なる場所の歩行者用信号の映り込み
* 対象信号の一つ向う側にある歩行者信号の映り込み
* 信号機の種類

<img src=https://upload.wikimedia.org/wikipedia/commons/a/a3/%E6%AD%A9%E8%A1%8C%E8%80%85%E7%94%A8%E4%BF%A1%E5%8F%B7%E6%A9%9F%E3%83%BB%E4%BA%BA%E5%BD%A2%E3%81%AE%E5%A4%A7%E3%81%8D%E3%81%95%E6%AF%94%E8%BC%83%EF%BC%88%E4%B8%8A%EF%BC%9A%E8%B5%A4%E3%80%81%E4%B8%8B%EF%BC%9A%E9%9D%92%E3%80%81%E5%B7%A6%E3%82%88%E3%82%8A%E9%9B%BB%E7%90%83%E5%BC%8F%E3%83%BBLED%E5%BC%8F%E3%83%BBLED%E3%83%AC%E3%83%B3%E3%82%BA%E5%BC%8F%EF%BC%89.jpg width="400">

![歩行者用信号機](http://img01.naganoblog.jp/usr/holidayy/Signal02.JPG)

## その他

* 現在位置の通知
* 歩行者信号機のアイコン（人形）は各国で違う->入れ替え可能に
* 音声も入れ替え可能に
* 道案内

## 現在位置

[[Android] GPSで位置情報を取得するアプリを作る](https://akira-watson.com/android/gps.html)

[[iOS] 位置情報の取得 (Swift3編)](https://dev.classmethod.jp/smartphone/ios-corelocation-swift3/)

[[iOS] MapKitを使って”ジオコーディング・逆ジオコーディング”をやってみる](https://dev.classmethod.jp/smartphone/iphone/geocoding-use-mapkit/)

[Androidで位置情報を扱うときの3つのTips](https://qiita.com/kikuchy/items/c79241b0488cb40c1da6)

[ジオコーディングと逆ジオコーディングをする方法(Google Geocoding APIの使い方)](https://syncer.jp/how-to-use-geocoding-api)

[逆ジオコーディングをfinds.jpに乗り換えてみた](https://qiita.com/jkr_2255/items/225f0c53e54dc4f265d1)

[国土地理院 タイル座標確認ページ](https://maps.gsi.go.jp/development/tileCoordCheck.html)

## [合成音声](https://qiita.com/maKunugi/items/90cbefe97887470fb328)

iOS : [AVSpeechSynthesizer](https://developer.apple.com/documentation/avfoundation/avspeechsynthesizer)

Android : [TextToSpeech](https://developer.android.com/reference/android/speech/tts/TextToSpeech)


## 問題点

1. 日中は信号機中のアイコン（人）が判別できるが、夜間は光が拡散してアイコンの形が判別できない。→露出等の調整で対処可能か？
1. 西日本（商用電源周波数60Hz）では、LED信号機の信号が写ったり消えたりする。（昼間のみ。夜間は発生しない。夜間は光量が必要なのでシャッタースピードが遅くなるため発生しないのでは？）。
fpsの設定変更で対応可能と考えたが、機種により可不可があったり、変更可能であっても設定値が選択式であったりする（自由設定不可）。別途対策が必要。

![消失する信号](https://github.com/63rabbits/Under-construction/blob/master/Disappearing%20signal.gif)

**信号が徐々に消える理由**：カメラの30fps（フレームレート）は公称であり、厳密には29.97fpsである。30fpsでは理論的に信号が写る/写らないかのいずれかであるが、実際は29.97fpsであるため徐々にタイミングがズレて写ったり写らなかったりする。( [fpsとHzと点滅周期の関係](https://mofulog.blogspot.com/2017/12/Dashcam-TrafficSignal-Lost.html#chapter-12)、 [検証グラフ](https://www.desmos.com/calculator/qnktlmbld1))

→シャッタースピードを遅くする（必要ならISO感度を下げる）ことで解決するか？

※環境:iPad mini 2 : 5Mpixel 1080p/30fps動画撮影


## スマホによる動画撮影について

動画撮影で制御できるパラメータは下記。

※スマホの絞り(f値)は固定されているので制御不可。(f値は仕様書に明記されている)

* ○　シャッタースピード
* ☓　絞り(f値)
* ○　ISO感度

[スマートフォンのカメラ画質がどのように決まるのかをカメラの基本原理から解説](https://gigazine.net/news/20150915-how-smartphone-camera-work/#group=nogroup&photo=3)


