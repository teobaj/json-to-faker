<script lang="ts">
  import { onMount } from "svelte";
  import { error, jsonData } from "./store";
  const topWrapper = " { ";
  let data = "";

  const transform = (jsonString: string) => {
    try {

      if (jsonString && jsonString !== "") {
        const parsed = JSON.parse(jsonString);
        Object.entries(parsed).forEach(([key, value]) => {
          if (fakerMapping[typeof value]) {
            parsed[key] = fakerMapping[typeof value](key, value);
          } else {
            parsed[key] = fakerMapping.default(key, value);
          }
        });
        
        data = JSON.stringify(parsed, undefined, 4);
        data = data.replaceAll('"faker', 'faker');
        data =data.replaceAll(')"', ')')
      }
    } catch (e) {
      error.set(e.message)
    }
  };

  const fakerMapping = {
    string: (key: string, value: string) => {
      if (key.toLowerCase().includes("id")) {
        return 'faker.random.numeric().toString()';
      }
      if (key.toLowerCase().includes("name")) {
        return 'faker.name.fullName()';
      }
      if (key.toLowerCase().includes("date")) {
        return 'faker.date.recent().toISOString().split("T")[0]';
      }
      if (key.toLowerCase().includes("branch")) {
        return 'faker.git.branch()';
      }
      return 'faker.lorem.lines()';
    },
    number: (key: string, value: number) => {
      return 'faker.random.numeric(' + value.toString().length + ')';
    },
    boolean: (key: string, value: boolean) => {
      return 'faker.datatype.boolean()';
    },
    default: (key: string, value: any) => {
      return 'faker.lorem.lines()';
    },
  };
  const copyToClipboard = () => {
    navigator.clipboard.writeText(data)
  }

  const handleMessages = (e: MessageEvent<any>) => {
    if(e.data === 'copyToClipboard') {
        copyToClipboard()
      }
  }

  onMount(() => {
    window.addEventListener('message', handleMessages)
    return () => {
      window.removeEventListener('message', handleMessages)
    } 
  })

  $: console.log($error)
  $: transform($jsonData);
</script>

<div class="wrapper">
  <div class="small">
    <pre>
      <code>
        {data}
      </code>    
    </pre>
  </div>
</div>


<style>
  code {
    display: flex;
  }
  .wrapper {
    height: 100%;
    width: 100%;
    display: grid;
    place-items: center;
  }
  .small {
    height: 90%;
    width: 90%;
    overflow: auto;
    border: 2px solid #710686;
    padding: 0.25rem;
  }
</style>