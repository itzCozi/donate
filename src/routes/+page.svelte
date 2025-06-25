<script>
  import { CopyCheck, Moon, Sun } from "lucide-svelte";
  import { onMount } from "svelte";

  let isPopupVisible = false;
  let darkMode = false;

  const btcAddress = "bc1qzae405taw3epjugns3anhh8urvaefn2j6xue34";
  const ethAddress = "0x179759aF5Df9419EE3C0d13D3Ecbf44ccbF66055";
  const xmrAddress =
    "4AUzCAtTAPa6DGV9NkyHHf7fhrayoN7o5XSCeQfhv4AiMdDkNCMjcsbVs49dThJtsPHt4bR2qupTUWyf44vScYqLCkueWej";

  function isNightTime() {
    const hour = new Date().getHours();
    return hour >= 20 || hour < 6;
  }

  function truncateAddress(address) {
    return address.length > 42 ? address.substring(0, 42) + "..." : address;
  }

  function copyToClipboard(textToCopy) {
    navigator.clipboard
      .writeText(textToCopy)
      .then(() => {
        isPopupVisible = true;
        setTimeout(() => {
          isPopupVisible = false;
        }, 3000);
      })
      .catch((err) => {
        console.error("Failed to copy text: ", err);
      });
  }

  function toggleDarkMode() {
    darkMode = !darkMode;
    if (typeof window !== "undefined") {
      updateDarkMode();
    }
  }

  function updateDarkMode() {
    if (darkMode) {
      document.documentElement.classList.add("dark");
      document.documentElement.style.setProperty("--background-color", "#121212");
    } else {
      document.documentElement.classList.remove("dark");
      document.documentElement.style.setProperty("--background-color", "#ffffff");
    }
  }

  onMount(() => {
    if (typeof window !== "undefined") {
      darkMode = isNightTime();
      updateDarkMode();
    }
  });
</script>

<div
  class="items-center justify-center"
  class:dark={darkMode}>
  <button
    class="fixed top-4 right-4 p-3 rounded-full hover:scale-105 transition duration-200"
    on:click={toggleDarkMode}
    title={darkMode ? "Switch to Light Mode" : "Switch to Dark Mode"}>
    {#if darkMode}
      <Sun class="h-6 w-6" />
    {:else}
      <Moon class="h-6 w-6" />
    {/if}
  </button>

  {#if isPopupVisible}
    <div class="popup">
      <div class="flex items-center justify-center flex-row gap-2">
        <CopyCheck class="h-5 w-auto" />
        Copied to clipboard
      </div>
    </div>
  {/if}
  <div class="mx-auto block">
    <div class="flex-1 flex flex-col gap-3 p-3">
      <h1
        id="how-to"
        class="flex flex-row gap-2 justify-center items-center relative">
        Donations
      </h1>

      <p class="dark:text-gray-300">
        Hello, first things first, I don't expect any donations. I build projects for the community
        for fun and look to get nothing in return. But if you want to support me and keep these
        projects running, you can do so by donating. However, I only accept crypto donations; I
        don't accept any other payment methods unfortunately.
      </p>

      <div>
        <h3 class="dark:text-gray-200">By donating you are supporting:</h3>
        <ul class="dark:text-gray-300">
          <li>
            <a
              href="https://sub.wyzie.ru"
              rel=""
              target="_blank">Wyzie Sub(title)s</a>
          </li>
          <li>
            <a
              href="https://wyzie.ru"
              rel=""
              target="_blank">The Wyzie API</a>
          </li>
          <li>
            <a
              href="https://github.com/sussy-code"
              rel=""
              target="_blank">Sudo-Flix</a>
          </li>
          <li>
            <a
              href="https://bookracy.org"
              rel=""
              target="_blank">Bookracy</a>
          </li>
          <li>
            <a
              href="https://markd.it"
              rel=""
              target="_blank">Markd.it</a>
          </li>
          <li>
            <a
              href="https://bye.undi.rest"
              rel=""
              target="_blank">Stremio Guide</a>
          </li>
          <li>
            <a
              href="https://github.com/itzcozi/i6.shark"
              rel=""
              target="_blank">i6.shark</a>
          </li>
          <li>
            <a
              href="https://365.ilysm.nl"
              rel=""
              target="_blank">365 Radio</a>
          </li>
        </ul>
        <p class="text-xs text-type-dimmed dark:text-gray-400">
          All of these projects are open source and free to use.
        </p>
      </div>

      <div class="flex justify-between items-center gap-2 mb-2 mt-1">
        <div class="flex flex-col">
          <h2 class="text-center">Bitcoin Address</h2>
          <div
            role="button"
            tabindex="0"
            on:click={() => copyToClipboard(btcAddress)}
            on:keydown={(e) => e.key === "Enter" && copyToClipboard(btcAddress)}
            title="Copy Bitcoin Address"
            class="flex flex-row gap-2 items-center text-sm hover:text-blue-500 dark:hover:text-blue-400 transition duration-200 break-all cursor-pointer">
            {truncateAddress(btcAddress)}
          </div>
        </div>
        <div class="flex flex-col">
          <h2 class="text-center">Ethereum Address</h2>
          <div
            role="button"
            tabindex="0"
            on:click={() => copyToClipboard(ethAddress)}
            on:keydown={(e) => e.key === "Enter" && copyToClipboard(ethAddress)}
            title="Copy Ethereum Address"
            class="flex flex-row gap-2 items-center text-sm hover:text-blue-500 dark:hover:text-blue-400 transition duration-200 break-all cursor-pointer">
            {truncateAddress(ethAddress)}
          </div>
        </div>
        <div class="flex flex-col">
          <h2 class="text-center">Monero Address</h2>
          <div
            role="button"
            tabindex="0"
            on:click={() => copyToClipboard(xmrAddress)}
            on:keydown={(e) => e.key === "Enter" && copyToClipboard(xmrAddress)}
            title="Copy Monero Address"
            class="flex flex-row gap-2 items-center text-sm hover:text-blue-500 dark:hover:text-blue-400 transition duration-200 break-all cursor-pointer">
            {truncateAddress(xmrAddress)}
          </div>
        </div>
      </div>

      <div class="p-4 border border-[var(--border-color)] dark:border-opacity-70">
        <h3>Thank You!</h3>
        <p class="text-sm dark:text-gray-300">
          Your support makes it possible to continue developing these free, open-source projects.
          Every donation, no matter how small, is really deeply appreciated and helps keep these
          services running and up-to-date.
        </p>
      </div>
    </div>

    <footer class="text-center text-type-dimmed text-sm mt-auto py-4 dark:text-gray-400">
      <p class="flex flex-row justify-center items-center gap-2">
        <!-- svelte-ignore a11y_consider_explicit_label -->
        <a
          href="https://github.com/itzcozi"
          target="_blank"
          rel="noopener noreferrer"
          class="hover:scale-105 text-dark dark:text-gray-300 transition duration-200"
          title="Github">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 496 512"
            class="w-5 h-5 fill-current">
            <path
              d="M165.9 397.4c0 2-2.3 3.6-5.2 3.6-3.3 .3-5.6-1.3-5.6-3.6 0-2 2.3-3.6 5.2-3.6 3-.3 5.6 1.3 5.6 3.6zm-31.1-4.5c-.7 2 1.3 4.3 4.3 4.9 2.6 1 5.6 0 6.2-2s-1.3-4.3-4.3-5.2c-2.6-.7-5.5 .3-6.2 2.3zm44.2-1.7c-2.9 .7-4.9 2.6-4.6 4.9 .3 2 2.9 3.3 5.9 2.6 2.9-.7 4.9-2.6 4.6-4.6-.3-1.9-3-3.2-5.9-2.9zM244.8 8C106.1 8 0 113.3 0 252c0 110.9 69.8 205.8 169.5 239.2 12.8 2.3 17.3-5.6 17.3-12.1 0-6.2-.3-40.4-.3-61.4 0 0-70 15-84.7-29.8 0 0-11.4-29.1-27.8-36.6 0 0-22.9-15.7 1.6-15.4 0 0 24.9 2 38.6 25.8 21.9 38.6 58.6 27.5 72.9 20.9 2.3-16 8.8-27.1 16-33.7-55.9-6.2-112.3-14.3-112.3-110.5 0-27.5 7.6-41.3 23.6-58.9-2.6-6.5-11.1-33.3 2.6-67.9 20.9-6.5 69 27 69 27 20-5.6 41.5-8.5 62.8-8.5s42.8 2.9 62.8 8.5c0 0 48.1-33.6 69-27 13.7 34.7 5.2 61.4 2.6 67.9 16 17.7 25.8 31.5 25.8 58.9 0 96.5-58.9 104.2-114.8 110.5 9.2 7.9 17 22.9 17 46.4 0 33.7-.3 75.4-.3 83.6 0 6.5 4.6 14.4 17.3 12.1C428.2 457.8 496 362.9 496 252 496 113.3 383.5 8 244.8 8zM97.2 352.9c-1.3 1-1 3.3 .7 5.2 1.6 1.6 3.9 2.3 5.2 1 1.3-1 1-3.3-.7-5.2-1.6-1.6-3.9-2.3-5.2-1zm-10.8-8.1c-.7 1.3 .3 2.9 2.3 3.9 1.6 1 3.6 .7 4.3-.7 .7-1.3-.3-2.9-2.3-3.9-2-.6-3.6-.3-4.3 .7zm32.4 35.6c-1.6 1.3-1 4.3 1.3 6.2 2.3 2.3 5.2 2.6 6.5 1 1.3-1.3 .7-4.3-1.3-6.2-2.2-2.3-5.2-2.6-6.5-1zm-11.4-14.7c-1.6 1-1.6 3.6 0 5.9 1.6 2.3 4.3 3.3 5.6 2.3 1.6-1.3 1.6-3.9 0-6.2-1.4-2.3-4-3.3-5.6-2z"
            ></path>
          </svg>
        </a>
        <!-- svelte-ignore a11y_consider_explicit_label -->
        <a
          href="https://x.com/sudoflix"
          class="hover:scale-105 text-dark dark:text-gray-300 transition duration-200"
          title="Twitter">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 512 512"
            class="w-5 h-5 fill-current">
            <path
              d="M459.4 151.7c.3 4.5 .3 9.1 .3 13.6 0 138.7-105.6 298.6-298.6 298.6-59.5 0-114.7-17.2-161.1-47.1 8.4 1 16.6 1.3 25.3 1.3 49.1 0 94.2-16.6 130.3-44.8-46.1-1-84.8-31.2-98.1-72.8 6.5 1 13 1.6 19.8 1.6 9.4 0 18.8-1.3 27.6-3.6-48.1-9.7-84.1-52-84.1-103v-1.3c14 7.8 30.2 12.7 47.4 13.3-28.3-18.8-46.8-51-46.8-87.4 0-19.5 5.2-37.4 14.3-53 51.7 63.7 129.3 105.3 216.4 109.8-1.6-7.8-2.6-15.9-2.6-24 0-57.8 46.8-104.9 104.9-104.9 30.2 0 57.5 12.7 76.7 33.1 23.7-4.5 46.5-13.3 66.6-25.3-7.8 24.4-24.4 44.8-46.1 57.8 21.1-2.3 41.6-8.1 60.4-16.2-14.3 20.8-32.2 39.3-52.6 54.3z"
            ></path>
          </svg>
        </a>
        <!-- svelte-ignore a11y_consider_explicit_label -->
        <a
          href="mailto:dev@wyzie.ru"
          class="hover:scale-105 text-dark dark:text-gray-300 transition duration-200"
          title="Email">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 1920 1920"
            class="w-5 h-5 fill-current">
            <path
              d="M1920 428.266v1189.54l-464.16-580.146-88.203 70.585 468.679 585.904H83.684l468.679-585.904-88.202-70.585L0 1617.805V428.265l959.944 832.441L1920 428.266ZM1919.932 226v52.627l-959.943 832.44L.045 278.628V226h1919.887Z"
              fill-rule="evenodd"></path>
          </svg>
        </a>
      </p>
      <p class="mt-2">
        Created by
        <a
          href="https://github.com/itzcozi"
          class="font-semibold transition duration-100 underline"
          title="Developer Github link">BadDeveloper</a>
        with 💙
      </p>
    </footer>
  </div>
</div>
