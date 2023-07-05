---
layout: default
triggers:
  - benign
  - freqtone
  - ultrasound
  - backnoise
  - advperturb
  - rir
---

# TrojanRoom
This is the demo page for _TrojanRoom_ proposed in the paper "Devil in the Room: Triggering Audio Backdoors in the Physical World".

## Abstract
Recent years have witnessed deep learning techniques endowing modern audio systems with powerful abilities. However, the latest studies have revealed its strong reliance on training data raising serious threats from backdoor attacks. Different from most existing works validating the effectiveness of audio backdoors in the digital world, we observe the mismatch between the trigger and backdoor in the physical space by investigating the sound channel distortion. Inspired by this observation, this paper proposes _TrojanRoom_ to bridge the gap between digital and physical audio backdoor attacks. _TrojanRoom_ adopts room impulse response (RIR) as a physical trigger to enable injection-free backdoor activation. By synthesizing dynamic RIRs and poisoning a source class of samples during data augmentation, _TrojanRoom_ allows any adversary to launch an effective and stealthy attack using the specific impulse response in a room. The evaluation shows over 92% and 97% attack success on both state-of-the-art speech command recognition and speaker recognition systems with negligible impact on normal accuracy below 3% at a distance over 5m. The experiments also demonstrate that _TrojanRoom_ could bypass human inspection and voice liveness detection and resist trigger disruption and backdoor erasing.

## RIR Trigger
Existing audio backdoor attacks performs trigger injection **over the line** while ignoring the physical issues. Hence, these attacks degrade in the physical world where the triger is injected **over the air**. This is due to the sound channel distortion including ambient reverberation and noise, which break the connection between the distorted trigger and implanted backdoor.

<img width="800" src="/assets/img/over-the-air-line.png" alt="over-the-air and over-the-line activation">

To bridge the gap between digital and physical audio backdoor attacks, _TrojanRoom_ turns the sound channel itself as a trigger injection path, i.e., _channel as a trigger_. _TrojanRoom_ models the reverberation as a Room Impulse Response (RIR) and proposes a RIR-based physical trigger to enable an **effective**, **stealthy** and **injection-free** audio backdoor attack in the physical world. 

<img width="800" src="/assets/img/injection-free.png" alt="injection-free activation">

## Baselines Attacks
We compare _TrojanRoom_ with state-of-the-art audio backdoor attacks with different trigger designs:
- **FreqTone** injects a 500ms low-volume single-frequency tone of 1kHz at the end of speech
- **UltraSound** injects a 250ms ultrasound signal of 21kHz at the end of speech
- **BackNoise** injects a 200ms background noise at the beginning of speech
- **AdvPerturb** injects a 200ms adversarial perturbation at a random position of speech

Here is an example of benign sample (speech command "yes") and poisoned samples with different triggers:
<img width="1300" src="/assets/img/baseline.png" alt="baseline">

## Audio Samples
We provide the following benign and poisoned audio samples for comparing the stealthiness of different triggers in terms of human perception.

### Short Speech Command
<table>
  <tr>
    <th>Trigger</th>
    <th>Command "yes"</th>
    <th>Command "no"</th>
    <th>Command "right"</th>
  </tr>
  {% for trigger in page.triggers %}    
  <tr>
    <th>{{ trigger }}</th>
    <th><audio src="/assets/wav/{{trigger}}/speech0.wav" controls preload></audio></th>
    <th><audio src="/assets/wav/{{trigger}}/speech1.wav" controls preload></audio></th>
    <th><audio src="/assets/wav/{{trigger}}/speech2.wav" controls preload></audio></th>
  </tr>
  {% endfor %}
</table>

### Long Speaker Utterance

<table>
  <tr>
    <th>Trigger</th>
    <th>Speaker 0</th>
    <th>Speaker 1</th>
    <th>Speaker 2</th>
  </tr>
  {% for trigger in page.triggers %}    
  <tr>
    <th>{{ trigger }}</th>
    <th><audio src="/assets/wav/{{trigger}}/speaker0.wav" controls preload></audio></th>
    <th><audio src="/assets/wav/{{trigger}}/speaker1.wav" controls preload></audio></th>
    <th><audio src="/assets/wav/{{trigger}}/speaker2.wav" controls preload></audio></th>
  </tr>
  {% endfor %}
</table>