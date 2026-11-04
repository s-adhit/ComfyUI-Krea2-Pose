# ComfyUI Krea-2 Pose

ComfyUI nodes for using the Krea-2 Pose Control LoRA.

## Installation

Clone this repository into `ComfyUI/custom_nodes`:

    cd ComfyUI/custom_nodes
    git clone https://github.com/s-adhit/ComfyUI-Krea2-Pose.git

Install the dependencies using the same Python environment as ComfyUI:

    pip install -r ComfyUI-Krea2-Pose/requirements.txt

Then restart ComfyUI.

## Model

Download the Pose Control LoRA from:

https://huggingface.co/adhit-420/Krea-2-PoseControl-LoRA-checkpoints

Use:

`release/krea2-pose-control-mix025.safetensors`

## Workflows

Simple (existing all-in-one node): use `Krea2PoseGenerate` with the release artifact, Krea-2 Turbo, and Krea-2 Raw checkpoint selections. Feed it a project-format `pose_condition` from `Krea2PoseExtractor` or `Krea2PoseCondition`.

Composable: connect `Krea2PoseModelLoader` to `Krea2PoseSampler`. The loader selects and caches the same three checkpoints, while the sampler accepts its runtime plus prompt and pose condition. `Krea2PoseExtractor` can produce that condition from a reference image; `Krea2PoseCondition` validates an existing one.

Example workflow for the simple path:

`example_workflows/krea2_pose_from_reference.json`

The workflow takes a reference image, runs DWPose, converts the detected pose to the COCO-17 format used during training, and renders the PoseBridge conditioning image automatically.

The composable nodes only separate Krea-2 runtime loading from sampling. They do not provide native ComfyUI KSampler or `MODEL`-patching compatibility.

## Main project

Training code, evaluations, dataset details, and the full project:

https://github.com/s-adhit/krea2-pose-control-LoRA
