# JIS Custom Firmware / JISカスタムファームウェア

## Overview / 概要

This branch contains a custom firmware configuration for the JIS-layout NocFree & keyboard.

このブランチには、JIS配列のNocFree &向けカスタムファームウェア設定が含まれています。

## Important / 重要

- Flash `nocfree_and_left.uf2` to the physical left half.
- Flash `nocfree_and_right.uf2` to the physical right half.
- Always use the left and right UF2 files produced by the same build.

- 左の物理ユニットには `nocfree_and_left.uf2` を書き込みます。
- 右の物理ユニットには `nocfree_and_right.uf2` を書き込みます。
- 左右は必ず同じビルドで作成されたUF2を組にして使います。

## Current keymap notes / 現在のキー配列に関する注意

- The physical Half-width/Full-width key sends `GRAVE` (` / ~).
- The Eisu key is tap: Muhenkan; hold: Fn layer.
- The Kana key sends Henkan.

- 物理全角／半角キーは `GRAVE`（` / ~）を送信します。
- 英数キーは短押しで無変換、長押しでFnレイヤーです。
- かなキーは変換キーです。

## Build and recovery / ビルドと復旧

See [Build instructions](build.md) and [Recovery instructions](recovery.md).

[ビルド手順](build.md) と [復旧手順](recovery.md) を参照してください。
