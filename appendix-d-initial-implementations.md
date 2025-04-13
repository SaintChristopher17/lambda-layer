## Appendix D – Initial Implementations

Several logic-native tools have already been developed that build on the λ Layer foundation. These early implementations demonstrate how the declaration-based approach enables new kinds of applications.

### Trust Graph Explorer

The λTrust Graph Explorer is a visualization tool that reads trust events directly from the Ethereum event log and renders them as an interactive network:

```javascript
// Key implementation fragment
async function buildTrustGraph() {
const trustEvents = await ethereum.getLogs({
address: LAMBDA_TRUST_ADDRESS,
topics: [ethers.utils.id("Trust(address,address)")],
fromBlock: GENESIS_BLOCK
});

const graph = { nodes: new Set(), edges: [] };

trustEvents.forEach(event => {
const from = ethers.utils.getAddress('0x' + event.topics[1].slice(26));
const to = ethers.utils.getAddress('0x' + event.topics[2].slice(26));

graph.nodes.add(from);
graph.nodes.add(to);
graph.edges.push({ from, to, timestamp: event.blockTime });
});

return graph;
}
