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
With the emergence of large-scale pre-trained models and the privacy need of data availability and invisibility, the model training executor and data holder of an artificial intelligence system are separated. This induces an increasing threat of backdoor attacks, particularly in machine-learning-as-a-service scenarios. As a beneficiary of machine learning’s powerful capability, modern audio systems are also impacted. Existing studies focus on digital backdoor attacks, leaving the practical threat of audio backdoor attacks unknown. In this paper, we explore the sound channel distortion and verify the mismatch between the trigger and backdoor in the physical space. To this end, we propose _TrojanRoom_ to bridge the gap between digital and physical backdoor attacks. _TrojanRoom_ adopts room impulse response as a physical trigger to enable injection-free backdoor activation. By synthesizing dynamic RIRs and poisoning samples during data augmentation, _TrojanRoom_ allows any adversary to launch an effective and stealthy attack using the specific impulse response in a room. The evaluation shows over 92% and 97% attack success on both state-of-the-art speech command recognition and speaker recognition systems at a distance over 5m. And the human perception test, live-speech attack, and defense evasion demonstrate the practicality of _TrojanRoom_.

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