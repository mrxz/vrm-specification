# `VRMC_vrm.humanoid`

本文書では、 `VRMC_vrm` 拡張のうち `humanoid` フィールドについての仕様を示します。
`humanoid bone` の一覧を定義します。

```json
extensions.VRMC_vrm.humanoid = {
  "humanBones": {
    "hips": {
      "node": 1 // index of glTF.Node
    },
    "spine": {
      "node": 2
    },
    // 省略
  }
}
```

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [ヒューマノイドボーンの一覧](#%E3%83%92%E3%83%A5%E3%83%BC%E3%83%9E%E3%83%8E%E3%82%A4%E3%83%89%E3%83%9C%E3%83%BC%E3%83%B3%E3%81%AE%E4%B8%80%E8%A6%A7)
  - [胴](#%E8%83%B4)
  - [頭](#%E9%A0%AD)
  - [脚](#%E8%84%9A)
  - [腕](#%E8%85%95)
  - [指](#%E6%8C%87)
- [ヒューマノイドボーンの親子関係](#%E3%83%92%E3%83%A5%E3%83%BC%E3%83%9E%E3%83%8E%E3%82%A4%E3%83%89%E3%83%9C%E3%83%BC%E3%83%B3%E3%81%AE%E8%A6%AA%E5%AD%90%E9%96%A2%E4%BF%82)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## ヒューマノイドボーンの一覧

* ヒューマノイドボーンは VRM 内で同じものが複数存在してはいけません。

### 胴

| ボーン名前 | 必須 |  親ボーン  | 位置の目安 | 親ボーンの存在が必須 |                           備考                           |
| :--------- | :--- | :--------- | ---------- | -------------------- | -------------------------------------------------------- |
| hips       | 必須 | (root)     | 股間       |                      | 通常、このボーンだけが移動し、他のボーンは回転だけします |
| spine      | 必須 | hips       | 骨盤の上端 |                      |                                                          |
| chest      |      | spine      | 胸郭の下端 |                      | 0.X では必須だった                                       |
| upperChest |      | chest      |            | 必須                 | chest が存在する場合にのみ、このボーンは存在できます     |
| neck       |      | upperChest | 首の付け根 |                      | 0.X では必須だった                                       |

### 頭

| ボーン名前 | 必須 | 親ボーン | 位置の目安 | 親ボーンの存在が必須 |                                                                    備考                                                                     |
| :--------- | :--- | :------- | ---------- | -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| head       | 必須 | neck     | 首の上端   |                      |                                                                                                                                             |
| leftEye    |      | head     |            |                      | [`VRMC_vrm.lookAt` 視線制御(オプション)](#vrmc_vrmlookat-%E8%A6%96%E7%B7%9A%E5%88%B6%E5%BE%A1%E3%82%AA%E3%83%97%E3%82%B7%E3%83%A7%E3%83%B3) |
| rightEye   |      | head     |            |                      | [`VRMC_vrm.lookAt` 視線制御(オプション)](#vrmc_vrmlookat-%E8%A6%96%E7%B7%9A%E5%88%B6%E5%BE%A1%E3%82%AA%E3%83%97%E3%82%B7%E3%83%A7%E3%83%B3) |
| jaw        |      | head     |            |                      |                                                                                                                                             |

### 脚

|  ボーン名前   | 必須 |   親ボーン    |   位置の目安   | 親ボーンの存在が必須 | 備考 |
| :------------ | :--- | :------------ | -------------- | -------------------- | ---- |
| leftUpperLeg  | 必須 | hips          | 脚の付け根     |                      |      |
| leftLowerLeg  | 必須 | leftUpperLeg  | 膝             |                      |      |
| leftFoot      | 必須 | leftLowerLeg  | 足首           |                      |      |
| leftToes      |      | leftFoot      | 足の指の付け根 |                      |      |
| rightUpperLeg | 必須 | hips          | 脚の付け根     |                      |      |
| rightLowerLeg | 必須 | rightUpperLeg | 膝             |                      |      |
| rightFoot     | 必須 | rightLowerLeg | 足首           |                      |      |
| rightToes     |      | rightFoot     | 足の指の付け根 |                      |      |

### 腕

|  ボーン名前   | 必須 |   親ボーン    |  位置の目安  | 親ボーンの存在が必須 | 備考 |
| :------------ | :--- | :------------ | ------------ | -------------------- | ---- |
| leftShoulder  |      | upperChest    |              |                      |      |
| leftUpperArm  | 必須 | leftShoulder  | 上腕の付け根 |                      |      |
| leftLowerArm  | 必須 | leftUpperArm  | 肘           |                      |      |
| leftHand      | 必須 | leftLowerArm  | 手首         |                      |      |
| rightShoulder |      | upperChest    |              |                      |      |
| rightUpperArm | 必須 | rightShoulder | 上腕の付け根 |                      |      |
| rightLowerArm | 必須 | rightUpperArm | 肘           |                      |      |
| rightHand     | 必須 | rightLowerArm | 手首         |                      |      |

### 指

|       ボーン名前        | 必須 |        親ボーン         | 位置の目安 | 親ボーンの存在が必須 | 備考 |
| :---------------------- | :--- | :---------------------- | ---------- | -------------------- | ---- |
| leftThumbMetacarpal     |      | leftHand                |            |                      |      |
| leftThumbProximal       |      | leftThumbMetacarpal     |            | 必須                 |      |
| leftThumbDistal         |      | leftThumbProximal       |            | 必須                 |      |
| leftIndexProximal       |      | leftHand                |            |                      |      |
| leftIndexIntermediate   |      | leftIndexProximal       |            | 必須                 |      |
| leftIndexDistal         |      | leftIndexIntermediate   |            | 必須                 |      |
| leftMiddleProximal      |      | leftHand                |            |                      |      |
| leftMiddleIntermediate  |      | leftMiddleProximal      |            | 必須                 |      |
| leftMiddleDistal        |      | leftMiddleIntermediate  |            | 必須                 |      |
| leftRingProximal        |      | leftHand                |            |                      |      |
| leftRingIntermediate    |      | leftRingProximal        |            | 必須                 |      |
| leftRingDistal          |      | leftRingIntermediate    |            | 必須                 |      |
| leftLittleProximal      |      | leftHand                |            |                      |      |
| leftLittleIntermediate  |      | leftLittleProximal      |            | 必須                 |      |
| leftLittleDistal        |      | leftLittleIntermediate  |            | 必須                 |      |
| rightThumbMetacarpal    |      | rightHand               |            |                      |      |
| rightThumbProximal      |      | rightThumbMetacarpal    |            | 必須                 |      |
| rightThumbDistal        |      | rightThumbProximal      |            | 必須                 |      |
| rightIndexProximal      |      | rightHand               |            |                      |      |
| rightIndexIntermediate  |      | rightIndexProximal      |            | 必須                 |      |
| rightIndexDistal        |      | rightIndexIntermediate  |            | 必須                 |      |
| rightMiddleProximal     |      | rightHand               |            |                      |      |
| rightMiddleIntermediate |      | rightMiddleProximal     |            | 必須                 |      |
| rightMiddleDistal       |      | rightMiddleIntermediate |            | 必須                 |      |
| rightRingProximal       |      | rightHand               |            |                      |      |
| rightRingIntermediate   |      | rightRingProximal       |            | 必須                 |      |
| rightRingDistal         |      | rightRingIntermediate   |            | 必須                 |      |
| rightLittleProximal     |      | rightHand               |            |                      |      |
| rightLittleIntermediate |      | rightLittleProximal     |            | 必須                 |      |
| rightLittleDistal       |      | rightLittleIntermediate |            | 必須                 |      |

## ヒューマノイドボーンの親子関係

* ヒューマノイドボーンは親ボーンが決まっています。必須でない親ボーンが存在しない場合は、親ボーンの親ボーンを探してください。
* ヒューマノイドボーンの間にヒューマノイドボーンではないノードが入ることは許容されます(UpperLegとLowerLegの間にヒューマノイドボーンでないノードがあるなど)

hips を root として以下のような親子になります。

* root(ヒューマノイドボーンではない。原点)
  * hips
    * spine
      * (chest)
        * (upperChest)
          * (neck)
            * head
              * (leftEye)
              * (rightEye)
              * (jaw)
          * (leftShoulder)
            * leftUpperArm
              * leftLowerArm
                * leftHand
                  * (fingers) 省略
          * (rightShoulder)
            * rightUpperArm
              * rightLowerArm
                * rightHand
                  * (fingers) 省略
    * leftUpperLeg
      * leftLowerLeg
        * leftFoot
          * (leftToes)
    * rightUpperLeg
      * rightLowerLeg
        * rightFoot
          * (leftToes)
