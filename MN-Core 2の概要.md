# 公式情報
- [マニュアル](https://projects.preferred.jp/mn-core/assets/mncore2_dev_manual_ja.pdf)
- [エミュレータ環境](https://projects.preferred.jp/mn-core/assets/mncore2_emuenv_20240412.tar.xz)

# その他情報
- https://preferred-networks.connpass.com/event/309119/

# MN-Core 2 の構造
- ![図](mn2-core.drawio.svg)
- 各種メモリ:
    - PDM: 4 MiB
    - DRAM: 4 GiB
    - L2BM: 32 KiLongWords
    - L1BM: 8 KiLongWords
    - LM0, LM1 (Local Memory): 2 KiLongWords, 読み書き 2 LongWords/cycle
    - GRF0, GRF1 (General Register File): 256 LongWords, 読み書き 2 LongWords/cycle
    - Tレジスタ: 8 LongWords, 読み書き 2 LongWords/cycle
※1 LongWord = 64 bits

# プログラムのアセンブル・テスト
MN-Core 2 のプログラムは `.vsm` ファイル。
これを公式エミュレータ環境の zip ファイルに含まれている `assemble3` でアセンブルし、 `.asm` 形式にする。
`.asm` 形式のファイルを `gpfn3_package_main` でテストできる。
なお、 `assemble3`, `gpfn3_package_main` ともに Linux 用の実行ファイルなので、 Windows で実行する際には WSL が必要。

`sample.vsm` をアセンブルして `sample.asm` を作り、テスト出力を `dump.txt` に入れるコマンドの流れは以下のとおり。

```sh
$ ./assemble3 program.vsm > program.asm
$ ./gpfn3_package_main -i sample.asm -d dump.txt
```