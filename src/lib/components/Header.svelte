<script>
    import { onMount } from 'svelte';
    import BellIcon from '../assets/icons/navbar-icon/BellIcon.svelte';
    import MenuIcon from '../assets/icons/navbar-icon/MenuIcon.svelte';
    import userAvatar from '../assets/images/users/user.png';

    let menuToggler;
    onMount(() => {
        menuToggler.addEventListener('click', function(){
            document.querySelector('.sidebar').classList.toggle('show')
        })
    })
</script>

<header class="header">
    <div class="container-fluid">
        <div class="header__nav">
            <button type="button" class="header__nav__toggle" bind:this={menuToggler}>
                <svelte:component this={MenuIcon} />
            </button>
            <button type="button" class="header__nav__notification active">
                <span class="header__nav__notification__icon">
                    <svelte:component this={BellIcon} />
                </span>
            </button>
            <div class="header__nav__account">
                <figure class="header__nav__account__figure">
                    <img class="header__nav__account__figure__bg" src={userAvatar} alt="user" width="56" height="56" loading="lazy" draggable="false" />
                </figure>
                <span class="header__nav__account__text">Humza</span>
            </div>
        </div>
    </div>
</header>
<div class="header-gap"></div>

<style>
    :global(:root) {
		--header-height: 76px;
	}

    .header-gap{
        height: calc(var(--header-height) + var(--header-offset-top, 0px));
    }

    .header{
        --_padding-block: 10px;
        position: fixed;
        top: var(--header-offset-top, 0);
        right: 0;
        left: var(--sidebar-width);
        padding-top: var(--_padding-block);
        padding-bottom: var(--_padding-block);
        padding-left: var(--container-inline-padding, 0);
		padding-right: var(--container-inline-padding, 0);
    }

    .header__nav,
    .header__nav__account
    {
        display: flex;
        align-items: center;
    }

    .header__nav{
        gap: 24px;
    }

    .header__nav__toggle,
    .header__nav__notification
    {
        --_size: 36px;
        font-size: 20px;
        width: var(--_size);
        height: var(--_size);
        display: inline-flex;
        align-items: center;
        justify-content: center;
        background-color: #000000;
        border: 1px solid #333333;
        border-radius: 10px;
    }

    .header__nav__notification{
        margin-left: auto;
    }

    .header__nav__notification__icon{
        position: relative;
    }

    .active .header__nav__notification__icon::after{
        content: '';
        position: absolute;
        top: 0;
        right: 0;
        width: 9px;
        height: 9px;
        background-color: var(--color-primary);
        border: 1.5px solid #EBEBEB;
        border-radius: 50rem;
    }

    .header__nav__account{
        gap: 12px;
    }

    .header__nav__account__figure{
        --_size: 56px;
        position: relative;
        width: var(--_size);
        height: var(--_size);
        border-radius: 50rem;
        overflow: hidden;
    }

    .header__nav__account__figure__bg{
        position: absolute;
        inset: 0;
        width: 100%;
        height: 100%;
    }

    .header__nav__account__text{
        font-weight: 700;
    }

    @media (min-width: 992px){
        :global(:root) {
            --header-offset-top: 35px;
        }

        .header__nav__toggle{
            display: none;
        }

        .header__nav__notification{
            border-color: transparent;
        }
    }
    
</style>