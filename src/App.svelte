<script>
  import Drawer, {
    AppContent,
    Content,
    Header,
    Title,
    Subtitle,
    Scrim
  } from "@smui/drawer";
  import List, { Item, Text } from "@smui/list";
  import Button, { Label } from "@smui/button";
  import IconButton from "@smui/icon-button";
  import Textfield, { Input } from "@smui/textfield";
  import FloatingLabel from "@smui/floating-label";
  import LineRipple from "@smui/line-ripple";

  let workspaces = [
    {
      name: "DevChrome",
      hostnames: ["developer.chrome.com", "developer.chrome.com2"]
    },
    {
      name: "GitLab",
      hostnames: ["git.panaya.int/r/app/pmain", "git.panaya.int/r/app/pmain2"]
    }
  ];

  let newHostName = "";
  let [selectedWorkspace] = workspaces;

  function addHostname() {
    selectedWorkspace.hostnames = [...selectedWorkspace.hostnames, newHostName];
  }
</script>

<style>
  .drawer-container {
    position: relative;
    display: flex;
    height: 350px;
    max-width: 600px;
    border: 1px solid rgba(0, 0, 0, 0.1);
    overflow: hidden;
    z-index: 0;
  }
  .main-content {
    padding: 16px;
    height: 100%;
    width: 100%;
    box-sizing: border-box;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }
  .url-list {
    overflow: auto;
    height: 350px;
  }
  .add-url-container {
    width: 100%;
    display: flex;
    justify-content: space-between;
  }
  .add-url-field {
    width: 100%;
  }
</style>

<h1>URL Workspaces</h1>

<svelte:head>
  <title>URL Workspaces</title>
</svelte:head>
<AppContent class="app-content">

  <div class="drawer-container">
    <Drawer>
      <Content>
        <List>
          {#each workspaces as workspace}
            <Item on:click={() => (selectedWorkspace = workspace)}>
              <Text>{workspace.name}</Text>
            </Item>
          {/each}
        </List>
      </Content>
    </Drawer>

    <main class="main-content">
      <div class="url-list">
        <h3>{selectedWorkspace.name}</h3>
        <List nonInteractive>
          {#each selectedWorkspace.hostnames as hostname}
            <Item>
              <Text>{hostname}</Text>
            </Item>
          {/each}
        </List>
      </div>
      <br />
      <div class="add-url-container">
        <Textfield
          withLeadingIcon
          variant="filled"
          fullwidth
          lineRipple={true}
          bind:value={newHostName}
          label="URL"
          type="url"
          class="add-url-field"
          input$aria-controls="helper-text-standard-a"
          input$aria-describedby="helper-text-standard-a" />
        <IconButton class="material-icons" on:click={addHostname}>
          add_to_photos
        </IconButton>
      </div>
    </main>
  </div>
</AppContent>
