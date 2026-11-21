<img src="assets/logo.png" width="112" height="112" alt="Blyx penguin lighting up the active stretch of an audio frame strip.">

# ActivitySpan

Locate active frames in a sequence of nonnegative signal levels. This Blyx library is part of the vision, audio and speech collection.

A brief pause inside an utterance can split a segment. Accept a caller-selected gap and preserve the original time axis. [librosa, splitting a signal into active intervals](https://librosa.org/doc/0.11.0/generated/librosa.effects.split.html)

## Install and run

Install [Blyx 0.2.1](https://www.blyx-lang.space/download) with a Rust toolchain and host linker for native builds.

```sh
git clone --depth 1 --branch v0.1.1 https://github.com/Rahulchaube1/blyx-activityspan.git
cd blyx-activityspan
blyxc native-run example.blyx
blyxc native-run tests.blyx
```

[Run the editable browser example](https://www.blyx-lang.space/play?example=package-activityspan) · [Package page](https://www.blyx-lang.space/packages/activityspan) · [Handbook](https://doc.blyx-lang.space/guide/linnet)

## Import the module

Run this in the directory containing your application's entry file.

```sh
git clone --depth 1 --branch v0.1.1 https://github.com/Rahulchaube1/blyx-activityspan.git vendor/activityspan
```

```blyx
use vendor::activityspan::activityspan;

fn main() {
    let levels = [0, 2, 0, 3, 0];
    let threshold = 1.0;
    let result = activityspan_bounds(levels, threshold);
    if len(result) == 0 { println!("invalid"); return; }
    let mut i = 0;
    while i < len(result) {
        println!(at(result, i));
        i += 1;
    }
}
```

Expected output

```text
1
4
2
```

## API

`activityspan_bounds(levels, threshold)`

Returns [first active index, exclusive final active index, active frames]. Silence returns [-1,-1,0]. Activity is strictly above threshold. Invalid arguments and nonfinite results return an empty vector. Integers carried in numeric vectors use the exact range from −(2^53−1) to 2^53−1.

| Argument | Domain |
| --- | --- |
| levels | Vector of values, each a nonnegative finite number |
| threshold | A nonnegative finite number |

## In use

[Linnet](https://github.com/Rahulchaube1/blyx-linnet) uses this module to summarize speech-activity intervals from a precomputed frame-level envelope.

## Verification and contributions

The regression suite in [tests.blyx](tests.blyx) checks the example, boundary cases and invalid inputs. Include a short reproducer and your compiler version in [an issue](https://github.com/Rahulchaube1/blyx-activityspan/issues). The source is dual-licensed under [MIT](LICENSE-MIT) or [Apache-2.0](LICENSE-APACHE). Read the [artwork notice](assets/NOTICE.txt) for credits.

## Connect with Rahul Chaube

[Portfolio](https://www.rahulchaube1.com/) · [GitHub](https://github.com/Rahulchaube1) · [LinkedIn](https://www.linkedin.com/in/rahulchaube1) · [Hugging Face](https://huggingface.co/oncody) · [X](https://x.com/RahulChaube_) · [EverestQ](https://www.everestqai.com/) · [Contact](https://www.rahulchaube1.com/contact)

[Blyx website](https://www.blyx-lang.space/) · [BlyxTorch](https://www.blyx-lang.space/packages/blyxtorch) · [Handbook](https://doc.blyx-lang.space/) · [Community](https://www.blyx-lang.space/community)

Support Rahul’s open-source work through [GitHub Sponsors](https://github.com/sponsors/Rahulchaube1) or [Buy Me a Coffee](https://buymeacoffee.com/rahulchaube).
