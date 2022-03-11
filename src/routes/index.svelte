<script>
import { fromBase58 } from "bip32";
import { networks, payments } from "liquidjs-lib";
let network = networks["liquid"];

let { p2wpkh, p2sh } = payments;

  let pubkey = 
    "xpub6DYVec9KiT6edxdocFAJmuiKe857uGJC3DTr1c4KMM5w9rQ4CnpH1AieDoSh332jK9dk4jFDD3SmaWhFPdyxoSJAQNYjX1jzJvyAAQf5R54";

  let root = fromBase58(pubkey,
    network
  );

  let address;
  let i = 0;
  let derive = () => {
    i++;
    let pubkey = root.derivePath(i.toString()).publicKey;
    let redeem = payments.p2wpkh({
      pubkey,
      network,
    });

    ({address} = payments.p2sh({
      redeem,
      network,
    }));
  }

  derive();

</script>

<button on:click={derive}>Get Address</button>
{address}
