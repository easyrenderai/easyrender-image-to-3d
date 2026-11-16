# easyrender-image-to-3d

Agent skill that turns one product photo into a textured 3D model (GLB) with [easyrender](https://easyrender.ai). The agent shows a free preview and the credit cost before a paid build.

This repository is the standalone copy of the skill package (MIT) from [`easyrenderai/easyrender.ai`](https://github.com/easyrenderai/easyrender.ai/tree/main/skills/easyrender-image-to-3d). It exists so directories such as skills.sh can list the skill from a repository name without a dot.

## Install

```sh
npx skills add easyrenderai/easyrender-image-to-3d
```

Installation adds instructions. It does not connect an easyrender account or spend credits. Connect the MCP server first:

```sh
claude mcp add --transport http easyrender https://easyrender.ai/api/mcp
```

Other clients, OAuth sign-in and API keys: [easyrender.ai/mcp](https://easyrender.ai/mcp#connect). Try: "Use the easyrender-image-to-3d skill to turn this photo into a GLB. Show me the preview and cost before spending any credits."

## License

MIT. See `LICENSE`. easyrender builds use account credits; see [current pricing](https://easyrender.ai/pricing).
