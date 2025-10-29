# Third-Party Licenses and Attributions

This document contains the licenses and attributions for all third-party software, models, and services used in Trilliano AI.

## Overview

Trilliano AI incorporates various open-source libraries, AI models, and third-party services. This document ensures proper attribution and compliance with all applicable licenses.

## Backend Dependencies

### Core Framework

#### FastAPI
- **License**: MIT License
- **Copyright**: Copyright (c) 2018 Sebastián Ramírez
- **Repository**: https://github.com/tiangolo/fastapi
- **Usage**: Web framework for backend API

```
MIT License

Copyright (c) 2018 Sebastián Ramírez

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

#### Uvicorn
- **License**: BSD 3-Clause License
- **Copyright**: Copyright (c) 2017-present, Encode OSS Ltd.
- **Repository**: https://github.com/encode/uvicorn
- **Usage**: ASGI server for FastAPI

#### SQLAlchemy
- **License**: MIT License
- **Copyright**: Copyright (c) 2006-2023 the SQLAlchemy authors and contributors
- **Repository**: https://github.com/sqlalchemy/sqlalchemy
- **Usage**: Database ORM and toolkit

#### Pydantic
- **License**: MIT License
- **Copyright**: Copyright (c) 2017 to present Pydantic Services Inc. and individual contributors
- **Repository**: https://github.com/pydantic/pydantic
- **Usage**: Data validation and settings management

### AI and Machine Learning

#### Hugging Face Transformers
- **License**: Apache License 2.0
- **Copyright**: Copyright 2018- The Hugging Face team
- **Repository**: https://github.com/huggingface/transformers
- **Usage**: Natural language processing models

```
Apache License
Version 2.0, January 2004
http://www.apache.org/licenses/

TERMS AND CONDITIONS FOR USE, REPRODUCTION, AND DISTRIBUTION

1. Definitions.

"License" shall mean the terms and conditions for use, reproduction,
and distribution as defined by Sections 1 through 9 of this document.

"Licensor" shall mean the copyright owner or entity granting the License.

"Legal Entity" shall mean the union of the acting entity and all
other entities that control, are controlled by, or are under common
control with that entity. For the purposes of this definition,
"control" means (i) the power, direct or indirect, to cause the
direction or management of such entity, whether by contract or
otherwise, or (ii) ownership of fifty percent (50%) or more of the
outstanding shares, or (iii) beneficial ownership of such entity.

"You" (or "Your") shall mean an individual or Legal Entity
exercising permissions granted by this License.

"Source" form shall mean the preferred form for making modifications,
including but not limited to software source code, documentation
source, and configuration files.

"Object" form shall mean any form resulting from mechanical
transformation or translation of a Source form, including but
not limited to compiled object code, generated documentation,
and conversions to other media types.

"Work" shall mean the work of authorship, whether in Source or
Object form, made available under the License, as indicated by a
copyright notice that is included in or attached to the work
(which shall not include communications that are clearly marked or
otherwise designated in writing by the copyright owner as "Not a Work").

"Derivative Works" shall mean any work, whether in Source or Object
form, that is based upon (or derived from) the Work and for which the
editorial revisions, annotations, elaborations, or other modifications
represent, as a whole, an original work of authorship. For the purposes
of this License, Derivative Works shall not include works that remain
separable from, or merely link (or bind by name) to the interfaces of,
the Work and derivative works thereof.

"Contribution" shall mean any work of authorship, including
the original version of the Work and any modifications or additions
to that Work or Derivative Works thereof, that is intentionally
submitted to Licensor for inclusion in the Work by the copyright owner
or by an individual or Legal Entity authorized to submit on behalf of
the copyright owner. For the purposes of this definition, "submitted"
means any form of electronic, verbal, or written communication sent
to the Licensor or its representatives, including but not limited to
communication on electronic mailing lists, source code control
systems, and issue tracking systems that are managed by, or on behalf
of, the Licensor for the purpose of discussing and improving the Work,
but excluding communication that is conspicuously marked or otherwise
designated in writing by the copyright owner as "Not a Contribution."

2. Grant of Copyright License. Subject to the terms and conditions of
this License, each Contributor hereby grants to You a perpetual,
worldwide, non-exclusive, no-charge, royalty-free, irrevocable
copyright license to use, reproduce, modify, display, perform,
sublicense, and distribute the Work and such Derivative Works in
Source or Object form.

3. Grant of Patent License. Subject to the terms and conditions of
this License, each Contributor hereby grants to You a perpetual,
worldwide, non-exclusive, no-charge, royalty-free, irrevocable
(except as stated in this section) patent license to make, have made,
use, offer to sell, sell, import, and otherwise transfer the Work,
where such license applies only to those patent claims licensable
by such Contributor that are necessarily infringed by their
Contribution(s) alone or by combination of their Contribution(s)
with the Work to which such Contribution(s) was submitted. If You
institute patent litigation against any entity (including a
cross-claim or counterclaim in a lawsuit) alleging that the Work
or a Contribution incorporated within the Work constitutes direct
or contributory patent infringement, then any patent licenses
granted to You under this License for that Work shall terminate
as of the date such litigation is filed.

4. Redistribution. You may reproduce and distribute copies of the
Work or Derivative Works thereof in any medium, with or without
modifications, and in Source or Object form, provided that You
meet the following conditions:

(a) You must give any other recipients of the Work or
    Derivative Works a copy of this License; and

(b) You must cause any modified files to carry prominent notices
    stating that You changed the files; and

(c) You must retain, in the Source form of any Derivative Works
    that You distribute, all copyright, trademark, patent,
    attribution notices from the Source form of the Work,
    excluding those notices that do not pertain to any part of
    the Derivative Works; and

(d) If the Work includes a "NOTICE" file as part of its
    distribution, then any Derivative Works that You distribute must
    include a readable copy of the attribution notices contained
    within such NOTICE file, excluding those notices that do not
    pertain to any part of the Derivative Works, in at least one
    of the following places: within a NOTICE file distributed
    as part of the Derivative Works; within the Source form or
    documentation, if provided along with the Derivative Works; or,
    within a display generated by the Derivative Works, if and
    wherever such third-party notices normally appear. The contents
    of the NOTICE file are for informational purposes only and
    do not modify the License. You may add Your own attribution
    notices within Derivative Works that You distribute, alongside
    or as an addendum to the NOTICE text from the Work, provided
    that such additional attribution notices cannot be construed
    as modifying the License.

You may add Your own copyright notice to Your modifications and
may provide additional or different license terms and conditions
for use, reproduction, or distribution of Your modifications, or
for any such Derivative Works as a whole, provided Your use,
reproduction, and distribution of the Work otherwise complies with
the conditions stated in this License.

5. Submission of Contributions. Unless You explicitly state otherwise,
any Contribution intentionally submitted for inclusion in the Work
by You to the Licensor shall be under the terms and conditions of
this License, without any additional terms or conditions.
Notwithstanding the above, nothing herein shall supersede or modify
the terms of any separate license agreement you may have executed
with Licensor regarding such Contributions.

6. Trademarks. This License does not grant permission to use the trade
names, trademarks, service marks, or product names of the Licensor,
except as required for reasonable and customary use in describing the
origin of the Work and reproducing the content of the NOTICE file.

7. Disclaimer of Warranty. Unless required by applicable law or
agreed to in writing, Licensor provides the Work (and each
Contributor provides its Contributions) on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or
implied, including, without limitation, any warranties or conditions
of TITLE, NON-INFRINGEMENT, MERCHANTABILITY, or FITNESS FOR A
PARTICULAR PURPOSE. You are solely responsible for determining the
appropriateness of using or redistributing the Work and assume any
risks associated with Your exercise of permissions under this License.

8. Limitation of Liability. In no event and under no legal theory,
whether in tort (including negligence), contract, or otherwise,
unless required by applicable law (such as deliberate and grossly
negligent acts) or agreed to in writing, shall any Contributor be
liable to You for damages, including any direct, indirect, special,
incidental, or consequential damages of any character arising as a
result of this License or out of the use or inability to use the
Work (including but not limited to damages for loss of goodwill,
work stoppage, computer failure or malfunction, or any and all
other commercial damages or losses), even if such Contributor
has been advised of the possibility of such damages.

9. Accepting Warranty or Additional Liability. When redistributing
the Work or Derivative Works thereof, You may choose to offer,
and charge a fee for, acceptance of support, warranty, indemnity,
or other liability obligations and/or rights consistent with this
License. However, in accepting such obligations, You may act only
on Your own behalf and on Your sole responsibility, not on behalf
of any other Contributor, and only if You agree to indemnify,
defend, and hold each Contributor harmless for any liability
incurred by, or claims asserted against, such Contributor by reason
of your accepting any such warranty or additional liability.

END OF TERMS AND CONDITIONS
```

#### PyTorch
- **License**: BSD 3-Clause License
- **Copyright**: Copyright (c) 2016-     Facebook, Inc
- **Repository**: https://github.com/pytorch/pytorch
- **Usage**: Deep learning framework

#### Diffusers
- **License**: Apache License 2.0
- **Copyright**: Copyright 2022 The HuggingFace Team
- **Repository**: https://github.com/huggingface/diffusers
- **Usage**: Diffusion models for image generation

#### OpenAI Whisper
- **License**: MIT License
- **Copyright**: Copyright (c) 2022 OpenAI
- **Repository**: https://github.com/openai/whisper
- **Usage**: Speech recognition

```
MIT License

Copyright (c) 2022 OpenAI

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

#### Coqui TTS
- **License**: Mozilla Public License 2.0
- **Copyright**: Copyright (c) 2021 Coqui GmbH
- **Repository**: https://github.com/coqui-ai/TTS
- **Usage**: Text-to-speech synthesis

## Frontend Dependencies

### Core Framework

#### React Native
- **License**: MIT License
- **Copyright**: Copyright (c) Meta Platforms, Inc. and affiliates
- **Repository**: https://github.com/facebook/react-native
- **Usage**: Mobile app framework

```
MIT License

Copyright (c) Meta Platforms, Inc. and affiliates.

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

#### Expo
- **License**: MIT License
- **Copyright**: Copyright (c) 2015-present 650 Industries, Inc. (aka Expo)
- **Repository**: https://github.com/expo/expo
- **Usage**: React Native development platform

#### React Navigation
- **License**: MIT License
- **Copyright**: Copyright (c) 2017 React Navigation Contributors
- **Repository**: https://github.com/react-navigation/react-navigation
- **Usage**: Navigation library for React Native

#### Framer Motion
- **License**: MIT License
- **Copyright**: Copyright (c) 2018 Framer B.V.
- **Repository**: https://github.com/framer/motion
- **Usage**: Animation library

### UI and Animation

#### Lottie React Native
- **License**: Apache License 2.0
- **Copyright**: Copyright 2017 Airbnb, Inc.
- **Repository**: https://github.com/lottie-react-native/lottie-react-native
- **Usage**: Animation rendering

#### React Native Reanimated
- **License**: MIT License
- **Copyright**: Copyright (c) 2016 Software Mansion
- **Repository**: https://github.com/software-mansion/react-native-reanimated
- **Usage**: Advanced animations

#### React Native Gesture Handler
- **License**: MIT License
- **Copyright**: Copyright (c) 2016 Software Mansion
- **Repository**: https://github.com/software-mansion/react-native-gesture-handler
- **Usage**: Gesture recognition

### Audio and Media

#### Expo AV
- **License**: MIT License
- **Copyright**: Copyright (c) 2015-present 650 Industries, Inc.
- **Repository**: https://github.com/expo/expo
- **Usage**: Audio and video playback

#### React Native Audio Recorder Player
- **License**: MIT License
- **Copyright**: Copyright (c) 2018 dooboolab
- **Repository**: https://github.com/dooboolab/react-native-audio-recorder-player
- **Usage**: Audio recording and playback

## AI Models and Services

### Stable Diffusion
- **License**: CreativeML Open RAIL-M License
- **Copyright**: Copyright (c) 2022 Robin Rombach and Patrick Esser and contributors
- **Repository**: https://github.com/CompVis/stable-diffusion
- **Usage**: Image generation model

```
CreativeML Open RAIL-M License

dated August 22, 2022

Section I: PREAMBLE

Multimodal generative models are being widely adopted and used, and have the potential to transform the way artists, among other individuals, conceive and benefit from AI or ML technologies as a tool for content creation.

Notwithstanding the current and potential benefits that these artifacts can bring to society at large, there are also concerns about potential misuses of them, either due to their technical limitations or ethical considerations.

In short, this license strives for both the open and responsible downstream use of the accompanying model. When it comes to the open character, we took inspiration from open source software licenses regarding the grant of IP rights. Referring to the downstream responsible use, we added use-based restrictions not permitting the use of the Model in very specific scenarios, in order for the licensor to be able to enforce the license in case potential misuses of the Model may occur.

At the same time, we strive to promote open and responsible research on generative models for art and content generation.

Even though downstream derivative versions of the model could be released under different licensing terms, the latter will always have to include - at minimum - the same use-based restrictions as the ones in the original license (this license). We refer to this as the "Use Restrictions Inheritance Principle".

Section II: DEFINITIONS

- "License" means the terms and conditions for use, reproduction, and Distribution as defined in this document.
- "Data" means a collection of information and/or content extracted from the dataset used with the Model, including to train, pretrain, or otherwise evaluate the Model. The Data is not licensed under this License.
- "Output" means the results of operating a Model as embodied in informational content resulting therefrom.
- "Model" means any accompanying machine-learning based assemblies (including checkpoints), consisting of learnt weights, parameters (including optimizer states), corresponding to the model architecture as embodied in the Complementary Material, that have been trained or tuned, in whole or in part, on the Data, using the Complementary Material.
- "Derivatives of the Model" means all modifications to the Model, works based on the Model, or any other model which is created or initialized by transfer of patterns of the weights, parameters, activations or outputs of the Model, to the other model, in order to cause the other model to perform similarly to the Model, including - but not limited to - distillation methods entailing the use of intermediate data representations or methods based on the generation of synthetic data by the Model for training the other model.
- "Complementary Material" means the accompanying source code and scripts used to define, run, load, benchmark or evaluate the Model, and used to prepare data for training or evaluation, if any. This includes any accompanying documentation, tutorials, examples, etc, if any.
- "Distribution" means any transmission, reproduction, publication or other sharing of the Model or Derivatives of the Model to a third party, including providing the Model as a hosted service made available by electronic or other remote means - e.g. API-based or web access.
- "Licensor" means the copyright owner or entity authorized by the copyright owner that is granting the License, including the persons or entities that may have rights in the Model and/or distributing the Model.
- "You" (or "Your") means an individual or Legal Entity exercising permissions granted by this License and/or making use of the Model for whichever purpose and in any field of use, including usage of the Model in an end-use application - e.g. chatbot, translator, image generator.
- "Third Parties" means individuals or legal entities that are not under common control with Licensor or You.
- "Contribution" means any work of authorship, including the original version of the Model and any modifications or additions to that Model or Derivatives of the Model thereof, that is intentionally submitted to Licensor for inclusion in the Model by the copyright owner or by an individual or Legal Entity authorized to submit on behalf of the copyright owner. For the purposes of this definition, "submitted" means any form of electronic, verbal, or written communication sent to the Licensor or its representatives, including but not limited to communication on electronic mailing lists, source code control systems, and issue tracking systems that are managed by, or on behalf of, the Licensor for the purpose of discussing and improving the Model, but excluding communication that is conspicuously marked or otherwise designated in writing by the copyright owner as "Not a Contribution."
- "Contributor" means Licensor and any individual or Legal Entity on behalf of whom a Contribution has been received by Licensor and subsequently incorporated within the Model.

Section III: CONDITIONS OF USAGE, DISTRIBUTION AND REDISTRIBUTION

1. Subject to the terms and conditions of this License, each Contributor hereby grants You a perpetual, worldwide, non-exclusive, no-charge, royalty-free, irrevocable copyright license to use, reproduce, modify, and distribute the Complementary Material, subject to the limitations set forth in paragraph 2 of this Section.

2. Distribution and Redistribution. You may reproduce and distribute copies of the Model or Derivatives of the Model thereof in any medium, with or without modifications, provided that You meet the following conditions:

a. Use-based restrictions as referenced in paragraph 5 of this License must be included as an enforceable provision by You in any type of legal agreement (e.g. a license) governing the use and/or distribution of the Model or Derivatives of the Model, and You shall give notice to subsequent users You Distribute to, that the Model or Derivatives of the Model are subject to paragraph 5 of this License. This provision does not apply to the use of Complementary Material.

b. You must give any other recipients of the Model or Derivatives of the Model a copy of this License;

c. You must cause any modified files to carry prominent notices stating that You changed the files;

d. You must retain, in the Source form of any Derivatives of the Model that You distribute, all copyright, patent, trademark, and attribution notices from the Source form of the Model, excluding those notices that do not pertain to any part of the Derivatives of the Model; You may add Your own copyright notice to Your modifications and may provide additional or different license terms and conditions - respecting paragraph 4.a. of this License - for use, reproduction, or Distribution of Your modifications, or for any such Derivatives of the Model as a whole, provided Your use, reproduction, and Distribution of the Model otherwise complies with the conditions stated in this License.

3. Each time You distribute or publicly display or publicly perform the Model or a Derivative of the Model, the Licensor offers to the recipient a license to the Model subject to this License.

4. You may add Your own copyright notice to Your modifications and may provide additional or different license terms and conditions for use, reproduction, or distribution of Your modifications, or for any such Derivatives of the Model as a whole, provided Your use, reproduction, and distribution of the Model otherwise complies with the conditions stated in this License.

5. Use Restrictions. The restrictions set forth in Attachment A are considered Use Restrictions. Therefore You cannot use the Model and the Derivatives of the Model for the specified restricted uses. You may use the Model subject to this License, including only for lawful purposes and in accordance with the License. Use may include creating any content with, finetuning, updating, running, training, evaluating and/or rederiving the Model.

6. The Output You Generate. Except as set forth herein, Licensor claims no rights in the Output You generate using the Model. You are accountable for the Output you generate and its subsequent uses. No use of the output can contravene any provision as stated in the License.

Section IV: OTHER PROVISIONS

1. The Complementary Material, which may contain components under different copyright notices and license terms, your use of the Complementary Material is subject to the terms and conditions of the contained license as provided in the corresponding files.

2. DISCLAIMER OF WARRANTY. UNLESS REQUIRED BY APPLICABLE LAW OR AGREED TO IN WRITING, LICENSOR PROVIDES THE MODEL AND THE COMPLEMENTARY MATERIAL (AND EACH CONTRIBUTOR PROVIDES ITS CONTRIBUTIONS) "AS IS", WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, EITHER EXPRESS OR IMPLIED, INCLUDING, WITHOUT LIMITATION, ANY WARRANTIES OR CONDITIONS OF TITLE, NON-INFRINGEMENT, MERCHANTABILITY, OR FITNESS FOR A PARTICULAR PURPOSE. YOU ARE SOLELY RESPONSIBLE FOR DETERMINING THE APPROPRIATENESS OF USING OR REDISTRIBUTING THE MODEL, DERIVATIVES OF THE MODEL, AND THE COMPLEMENTARY MATERIAL AND ASSUME ANY RISKS ASSOCIATED WITH YOUR USE OF THE MODEL, DERIVATIVES OF THE MODEL, AND THE COMPLEMENTARY MATERIAL.

3. LIMITATION OF LIABILITY. IN NO EVENT AND UNDER NO LEGAL THEORY, WHETHER IN TORT (INCLUDING NEGLIGENCE), CONTRACT, OR OTHERWISE, UNLESS REQUIRED BY APPLICABLE LAW (SUCH AS DELIBERATE AND GROSSLY NEGLIGENT ACTS) OR AGREED TO IN WRITING, SHALL ANY CONTRIBUTOR BE LIABLE TO YOU FOR DAMAGES, INCLUDING ANY DIRECT, INDIRECT, SPECIAL, INCIDENTAL, OR CONSEQUENTIAL DAMAGES OF ANY CHARACTER ARISING AS A RESULT OF THIS LICENSE OR OUT OF THE USE OR INABILITY TO USE THE MODEL AND THE COMPLEMENTARY MATERIAL (INCLUDING BUT NOT LIMITED TO DAMAGES FOR LOSS OF GOODWILL, WORK STOPPAGE, COMPUTER FAILURE OR MALFUNCTION, OR ANY AND ALL OTHER COMMERCIAL DAMAGES OR LOSSES), EVEN IF SUCH CONTRIBUTOR HAS BEEN ADVISED OF THE POSSIBILITY OF SUCH DAMAGES.

4. If any provision of this License is held to be invalid or unenforceable under applicable law, it shall not affect the validity or enforceability of the remainder of the terms of this License, and without further action by the parties hereto, such provision shall be reformed to the minimum extent necessary to make such provision valid and enforceable.

5. The term of this License will commence upon your acceptance of this License or access to the Model and will continue until terminated. Upon termination of this License, You shall delete and cease use of the Derivatives of the Model. Sections 2, 5 to 8 shall survive termination of this License.

6. This License shall be governed by and construed in accordance with the laws of the State of California. The application of the United Nations Convention on Contracts for the International Sale of Goods is expressly excluded.

Attachment A

Use Restrictions

You agree not to use the Model or Derivatives of the Model:
- In any way that violates any applicable national, federal, state, local or international law or regulation;
- For the purpose of exploiting, harming or attempting to exploit or harm minors in any way;
- To generate or disseminate verifiably false information and/or content with the purpose of harming others;
- To generate or disseminate personal identifiable information that can be used to harm an individual;
- To defame, disparage or otherwise harass others;
- For fully automated decision making that adversely affects an individual's legal rights or otherwise creates or modifies a binding, enforceable obligation;
- For any use intended to or which has the effect of discriminating against or harming individuals or groups based on online or offline social behavior or known or predicted personal or personality characteristics;
- To exploit any of the vulnerabilities of a specific group of persons based on their age, social, physical or mental characteristics, in order to materially distort the behavior of a person pertaining to that group in a manner that causes or is likely to cause that person or another person physical or psychological harm;
- For any use intended to or which has the effect of discriminating against individuals or groups based on legally protected characteristics or categories;
- To provide medical advice and medical results interpretation;
- To generate or disseminate information for the purpose to be used for administration of justice, law enforcement, immigration or asylum processes, such as predicting an individual will commit fraud/crime commitment (e.g. by text profiling, drawing causal relationships between assertions made in documents, indiscriminate and arbitrarily-targeted use).
```

### Large Language Models

Various LLM models may be used with different licenses:

#### Llama 2
- **License**: Custom License for Llama 2
- **Copyright**: Copyright (c) Meta Platforms, Inc.
- **Repository**: https://github.com/facebookresearch/llama
- **Usage**: Conversational AI model

#### Mistral 7B
- **License**: Apache License 2.0
- **Copyright**: Copyright (c) Mistral AI
- **Repository**: https://github.com/mistralai/mistral-src
- **Usage**: Language model

## Third-Party Services

### OpenAI API
- **Terms of Service**: https://openai.com/terms/
- **Privacy Policy**: https://openai.com/privacy/
- **Usage Policy**: https://openai.com/policies/usage-policies
- **Usage**: GPT models for text generation

### Anthropic API
- **Terms of Service**: https://www.anthropic.com/terms
- **Privacy Policy**: https://www.anthropic.com/privacy
- **Usage Policy**: https://www.anthropic.com/usage-policy
- **Usage**: Claude models for text generation

### Google AI API
- **Terms of Service**: https://ai.google.dev/terms
- **Privacy Policy**: https://policies.google.com/privacy
- **Usage**: Gemini models for text generation

### Replicate API
- **Terms of Service**: https://replicate.com/terms
- **Privacy Policy**: https://replicate.com/privacy
- **Usage**: Cloud-based AI model inference

## Fonts and Typography

### Orbitron Font
- **License**: SIL Open Font License 1.1
- **Copyright**: Copyright (c) 2009, Matt McInerney
- **Repository**: https://github.com/theleagueof/orbitron
- **Usage**: Heading font

```
SIL OPEN FONT LICENSE Version 1.1 - 26 February 2007

PREAMBLE
The goals of the Open Font License (OFL) are to stimulate worldwide
development of collaborative font projects, to support the font creation
efforts of academic and linguistic communities, and to provide a free and
open framework in which fonts may be shared and improved in partnership
with others.

The OFL allows the licensed fonts to be used, studied, modified and
redistributed freely as long as they are not sold by themselves. The
fonts, including any derivative works, can be bundled, embedded, 
redistributed and/or sold with any software provided that any reserved
names are not used by derivative works. The fonts and derivatives,
however, cannot be released under any other type of license. The
requirement for fonts to remain under this license does not apply
to any document created using the fonts or their derivatives.

DEFINITIONS
"Font Software" refers to the set of files released by the Copyright
Holder(s) under this license and clearly marked as such. This may
include source files, build scripts and documentation.

"Reserved Font Name" refers to any names specified as such after the
copyright statement(s).

"Original Version" refers to the collection of Font Software components as
distributed by the Copyright Holder(s).

"Modified Version" refers to any derivative made by adding to, deleting,
or substituting -- in part or in whole -- any of the components of the
Original Version, by changing formats or by porting the Font Software to a
new environment.

"Author" refers to any designer, engineer, programmer, technical
writer or other person who contributed to the Font Software.

PERMISSION & CONDITIONS
Permission is hereby granted, free of charge, to any person obtaining
a copy of the Font Software, to use, study, copy, merge, embed, modify,
redistribute, and sell modified and unmodified copies of the Font
Software, subject to the following conditions:

1) Neither the Font Software nor any of its individual components,
in Original or Modified Versions, may be sold by itself.

2) Original or Modified Versions of the Font Software may be bundled,
redistributed and/or sold with any software, provided that each copy
contains the above copyright notice and this license. These can be
included either as stand-alone text files, human-readable headers or
in the appropriate machine-readable metadata fields within text or
binary files as long as those fields can be easily viewed by the user.

3) No Modified Version of the Font Software may use the Reserved Font
Name(s) unless explicit written permission is granted by the corresponding
Copyright Holder. This restriction only applies to the primary font name as
presented to the users.

4) The name(s) of the Copyright Holder(s) or the Author(s) of the Font
Software shall not be used to promote, endorse or advertise any
Modified Version, except to acknowledge the contribution(s) of the
Copyright Holder(s) and the Author(s) or with their explicit written
permission.

5) The Font Software, modified or unmodified, in part or in whole,
must be distributed entirely under this license, and must not be
distributed under any other license. The requirement for fonts to
remain under this license does not apply to any document created
using the Font Software.

TERMINATION
This license becomes null and void if any of the above conditions are
not met.

DISCLAIMER
THE FONT SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO ANY WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT
OF COPYRIGHT, PATENT, TRADEMARK, OR OTHER RIGHT. IN NO EVENT SHALL THE
COPYRIGHT HOLDER BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY,
INCLUDING ANY GENERAL, SPECIAL, INDIRECT, INCIDENTAL, OR CONSEQUENTIAL
DAMAGES, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING
FROM, OUT OF THE USE OR INABILITY TO USE THE FONT SOFTWARE OR FROM
OTHER DEALINGS IN THE FONT SOFTWARE.
```

### Poppins Font
- **License**: SIL Open Font License 1.1
- **Copyright**: Copyright (c) 2014, Indian Type Foundry
- **Repository**: https://github.com/itfoundry/Poppins
- **Usage**: Body text font

## Development Tools

### Docker
- **License**: Apache License 2.0
- **Copyright**: Copyright 2013-2017 Docker, Inc.
- **Repository**: https://github.com/docker/docker-ce
- **Usage**: Containerization

### Node.js
- **License**: MIT License
- **Copyright**: Copyright Node.js contributors
- **Repository**: https://github.com/nodejs/node
- **Usage**: JavaScript runtime

### Python
- **License**: Python Software Foundation License
- **Copyright**: Copyright (c) 2001-2023 Python Software Foundation
- **Repository**: https://github.com/python/cpython
- **Usage**: Programming language

## Testing Libraries

### pytest
- **License**: MIT License
- **Copyright**: Copyright (c) 2004-2023 Holger Krekel and others
- **Repository**: https://github.com/pytest-dev/pytest
- **Usage**: Python testing framework

### Jest
- **License**: MIT License
- **Copyright**: Copyright (c) Meta Platforms, Inc. and affiliates
- **Repository**: https://github.com/facebook/jest
- **Usage**: JavaScript testing framework

### React Native Testing Library
- **License**: MIT License
- **Copyright**: Copyright (c) 2019 Callstack
- **Repository**: https://github.com/callstack/react-native-testing-library
- **Usage**: React Native component testing

## Compliance Notes

### License Compatibility

All included licenses are compatible with the MIT License under which Trilliano AI is released. The most restrictive licenses in our dependency chain are:

1. **CreativeML Open RAIL-M** (Stable Diffusion) - Includes use restrictions
2. **Mozilla Public License 2.0** (Coqui TTS) - Copyleft for modifications
3. **Apache License 2.0** (Various) - Patent grant requirements

### Attribution Requirements

When distributing Trilliano AI:

1. Include this THIRD_PARTY_LICENSES.md file
2. Maintain all copyright notices in source code
3. Include license texts for Apache 2.0 and other required licenses
4. Respect trademark restrictions (do not use third-party trademarks)

### Use Restrictions

Due to the Stable Diffusion CreativeML Open RAIL-M license, users must comply with the use restrictions listed in that license, including:

- No illegal or harmful content generation
- No exploitation of minors
- No generation of false information to harm others
- No medical advice generation
- No discriminatory uses

### Commercial Use

Most dependencies allow commercial use under their respective licenses. However:

- Some AI models may have specific commercial use restrictions
- Third-party API services have their own terms of service
- Users must obtain appropriate licenses for commercial deployment

### Updates and Maintenance

This document should be updated whenever:

- New dependencies are added
- Existing dependencies are updated to new versions
- License terms change for any dependency
- New third-party services are integrated

### Contact for License Questions

For questions about licensing and compliance:
- **Email**: legal@trillianoai.com
- **Subject**: License Compliance Inquiry

---

**Last Updated**: [DATE]  
**Document Version**: 1.0  
**Maintained by**: ₮ⱤłⱠⱠł₳₦Ø ₲ⱠØ฿₳Ⱡ Ɇ₥₱łⱤɆ Legal Team