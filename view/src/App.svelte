<script>
  import { Fullpage, FullpageSection, FullpageSlide } from 'svelte-fullpage'

  import Link from "./components/link.svelte"
  import Social from "./components/social.svelte"
  import Event from "./components/event.svelte"

  import Wave from "./components/wave.svelte"
  
  import ActionSlide from "./components/actionSlide.svelte"

  import linkFile from "./config/links.json"
  import socialFile from './config/socials.json'
  import eventFile from './config/events.json'
  import actionsFile from './config/actions.json'

  
  const sections = [
    "Accueil",
    "Événements à venir",
    "Nos modes d'action"
  ]

  //Must be manually updated to be able to access slides
  const slides = [
    'Introduction','Marches et manifestations','Actions de désobéissance civile',"Actions de sensibilisation","Soutien aux autres luttes"
  ]
</script>

<main>
  <Wave side="topleft" />
  <Wave side="bottomright" />

  <Fullpage {sections}>
    <FullpageSection center>
      <div class="section">
        <img class="part logo" src="/assets/logo.svg" alt="Fridays For Future Grenoble" />
        <div class="part links">
          <ul>
          {#each linkFile.links as link}
            <li><Link content="{link.content.toLocaleUpperCase()}" link="{link.link}" /></li>
          {/each}
          </ul>
        </div>
        <div class="part socials">
          {#each socialFile.socials as social}
            <Social icon="{social.icon}" link="{social.link}" />
          {/each}
        </div>
      </div>
    </FullpageSection>
    <FullpageSection center>
      <div class="section">
        <div class="part events">
          <h2 class="events title">ÉVÉNEMENTS À VENIR :</h2>
          <ul>
              {#each eventFile.events as event}
                <li class="event"><Event title={event.title} date={event.date} time={event.time} place={event.place} link={event.link}/></li>
              {/each}
          </ul>
        <div>
      </div>
    </FullpageSection>
    <FullpageSection center {slides} arrows>
      {#each actionsFile.actions as action}
        <ActionSlide {...action}/>
      {/each}
    </FullpageSection>
  </Fullpage>

</main>

<style>
	main {
		position: absolute;
		left: 0; right: 0;
		top: 0; bottom: 0;

    display: flex;
    justify-content: center;
    align-items: center;
	}

  .logo {
    max-width: 350px;
  }

  .section {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    max-width: 550px;
  }

  .section .part {
    margin-top: 15px;
    margin-bottom: 15px;
  }

  ul {
    list-style: none;
    padding: 0;
  }

  .events{
    width: 95%;
  }


  @media only screen and (max-width: 600px) {
    .logo {
      max-width: 250px;
    }

    .section {
      margin: 15px;
    }
  }

  @media only screen and (max-width: 540px) {
     .title {
      font-size: 30px;
    }
  }

  @media only screen and (max-height: 520px) {
    .part {
      margin-top: 0px;
      margin-bottom: 0px;
    }
  }

  @media only screen and (max-width: 330px) {
    .title {
      font-size: 20px;
    }
  }
</style>