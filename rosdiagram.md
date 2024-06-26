```mermaid
%%{
  init: {
    'theme': 'base',
    'themeVariables': {
      'primaryColor': '#D3D3D3',
      'primaryTextColor': '#000000',
      'primaryBorderColor': '#D3D3D3',
      'lineColor': '#D3D3D3',
      'secondaryColor': '#D3D3D3',
      'tertiaryColor': '#fff'
    }
  }
}%%sequenceDiagram
    participant NM as "NodeMonitor"
    participant RN as "ROS Node"
    participant Pub as "Publisher (/alive_nodes)"
    participant Sub as "Subscriber (/alive_nodes)"
    participant TM as "Create Consensus"
    participant PHM as "PHM Tool"
    
    NM->>RN: Check ROS Nodes Status
    RN-->>NM: Status Response
    NM->>Pub: Publish Local Alive Nodes
    Pub->>Sub: Alive Nodes Message
    Sub->>NM: Receive Global Alive Nodes
    NM->>TM: Send Local Consensus 
    TM->>NM: Analyze Global Consensus (Interval)
    TM->>PHM: Send Consensus to PHM
    PHM-->>NM: Monitor and Respond

