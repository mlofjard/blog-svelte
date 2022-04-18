<script lang="ts">
    import { link } from "svelte-navigator";
</script>

<div class="container">
    <nav>
        <ul>
            <li class="code"><a href="/topic/code" use:link>Code</a></li>
            <li class="life"><a href="/topic/life" use:link>Life</a></li>
            <li class="fun"><a href="/topic/fun" use:link>Fun</a></li>
        </ul>
    </nav>
    <div class="content"><slot /></div>
    <footer>
        <ul>
            <li class="source"><a href="/source" use:link>Source</a></li>
            <li class="archive"><a href="/archive" use:link>Archive</a></li>
            <li class="about"><a href="/about" use:link>About</a></li>
        </ul>
        <div class="copy">&#169; 2022 Mikael Lofj&auml;rd</div>
    </footer>
</div>


<style lang="scss">
    @import "../styles/variables.scss";
  
    :global(body) {
      background-color: $color-white;
      font-family: "Open Sans", sans-serif;
      font-weight: 300;
      font-size: 1rem;
    }
  
    .container {
      display: flex;
      flex-direction: column;
      min-height: 100vh;
    }
  
    nav {
      //margin-bottom: 2.4rem;
      position: sticky;
      top: 0;
      left: 0;
      //    background-color: $color-dark;
      background-image: linear-gradient(0deg, #1b1b1b 0%, $color-dark 100%);
      //box-shadow: 0 -20px 16px 20px rgba(0, 0, 0, 0.3), 0 0 20px 20px $color-white;
      display: flex;
      flex-direction: column;
      align-items: center;
      z-index: 1;
      height: 39px;
  
      > ul {
        display: flex;
  
        > li {
          display: block;
          margin: 0;
          padding: 0;
  
          > a {
            display: inline-block;
            text-decoration: none;
            padding: 0.8rem 1.6rem;
            margin: 0;
            font-weight: 600;
            color: $color-white;
            text-transform: uppercase;
            font-size: 0.8rem;
            line-height: 0.8rem;
            background-image: linear-gradient(0deg, #000 100%, transparent 100%);
            background-position: left 0 bottom -2rem;
            background-repeat: no-repeat;
            transition: background 300ms ease-in-out, color 300ms ease-in-out;
  
            &:hover {
              background-position: left 0 bottom 0;
            }
  
            &::first-letter {
              font-size: 120%;
            }
          }
        }
  
        > li.code > a {
          background-image: linear-gradient(
            0deg,
            $color-blue 100%,
            transparent 100%
          );
        }
  
        > li.life > a {
          background-image: linear-gradient(
            0deg,
            $color-yellow 100%,
            transparent 100%
          );
  
          &:hover {
            color: $color-dark;
          }
        }
  
        > li.fun > a {
          background-image: linear-gradient(
            0deg,
            $color-red 100%,
            transparent 100%
          );
        }
      }
    }
  
    footer {
      background-image: linear-gradient(0deg, #1b1b1b 0%, $color-dark 100%);
      //box-shadow: 0 -20px 16px 20px rgba(0, 0, 0, 0.3), 0 0 20px 20px $color-white;
      display: flex;
      flex-direction: row;
      align-items: center;
      justify-content: space-between;
      height: 24px;
  
      .copy {
        color: $color-white;
        font-size: .6rem;
        font-weight: 600;
        line-height: .6rem;
        text-transform: uppercase;
        padding-right: 1.2rem;
      }
  
      > ul {
        display: flex;
  
        > li {
          display: block;
          margin: 0;
          padding: 0;
  
          > a {
            display: inline-block;
            text-decoration: none;
            padding: 0.4rem 1.2rem .4rem 1.2rem;
            margin: 0;
            font-weight: 600;
            color: $color-white;
            text-transform: uppercase;
            font-size: 0.6rem;
            line-height: 0.6rem;
            background-image: linear-gradient(0deg, #000 100%, transparent 100%);
            background-position: left 0 bottom 1.3rem;
            background-repeat: no-repeat;
            transition: background 300ms ease-in-out, color 300ms ease-in-out;
  
            &:hover {
              background-position: left 0 bottom 0;
            }
  
            &::first-letter {
              font-size: 120%;
            }
          }
        }
  
        > li.source > a {
          background-image: linear-gradient(
            0deg,
            $color-blue 100%,
            transparent 100%
          );
        }
  
        > li.archive > a {
          background-image: linear-gradient(
            0deg,
            $color-yellow 100%,
            transparent 100%
          );
  
          &:hover {
            color: $color-dark;
          }
        }
  
        > li.about > a {
          background-image: linear-gradient(
            0deg,
            $color-red 100%,
            transparent 100%
          );
        }
      }
    }
  
    .content {
      //padding: 0 4rem 1.6rem 4rem;
      padding: 0;
      flex: 1;
      display: flex;
      max-height: calc(100vh - 39px - 24px);
      //flex-direction: row;
    }
  
    @media only screen and (max-width: 800px) {
      .content {
        padding: 0 0.8rem 2.4rem 0.8rem;
      }
    }
  </style>
  